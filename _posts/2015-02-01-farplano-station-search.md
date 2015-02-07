---
layout: post
title: "FarPlano: station search architecture"
date: 2015-02-01
comments: true
published: true
categories:
- farplano
tags:
- mongodb
- location search
---

Since its advent, all the functionality in **FarPlano** relied exclusively on the [HAFAS API](http://www.hacon.de/hafas-en) provided by Public Transport companies, including finding nearest location, searching location by query, retrieving stationboard, etc.

The generic architecture of the whole ecosystem is depicted on the image below:

<img alt="FarPlano Architecture" src="/images/blog/2015-02-01-farplano-station-search/architecture.svg" />

The use of the HAFAS API has its obvious advantages, such as the low implementation and maintenance costs, i.e. one just needs to implement a proxy interface that will interact with an API.
However, there are also a number of disadvantages of the proxy architecture, including the impossibility to alter location search process, longer response times and various peculiarities of the HAFAS API (that deserve a separate post).

The impossibility of changing the HAFAS's location search algorithm became the most crucial problem as we think it is possible to provide a better user satisfaction with other approaches.
For example, HAFAS search algorithm does not use the information about user's current location to search on the stations closes to him first.
That's why as our service continued to grow, we decided to implement our own station search algorithm.
Luckily, many public transport companies provide their data in the standard [General Transit Feed Specification (GTFS)](http://en.wikipedia.org/wiki/General_Transit_Feed_Specification) format[^1].

As a backend database, we decided to use [MongoDB](http://www.mongodb.org/) for the following reasons:

* the data is only meant to be consumed by a service and updated by a script one a week or so, hence we don't really need transaction support which will only slow things down;
* MongoDB natively supports [geo-spatial indexes](http://docs.mongodb.org/manual/core/geospatial-indexes/), which allows to efficiently perform nearest location searches;
* as in any document-oriented DB, data schema is flexible, which means we can add new fields or completely change document structure without hassle if necessary.

### Search algorithm

Now, efficient implementation of **location search algorithm** requires an efficient **autocomplete search** over the set of location names.
The state-of-the-art solution to this problem is a [Prefix Tree](http://en.wikipedia.org/wiki/Trie) or a similar data structure.
However, MongoDB does not support prefix trees natively, but we can implement it by generating prefixes ourselves.
At the core of the search algorithm there are the following three indexes:

* Full name prefixes (``full_index``), ``[f, fr, fri, ..., fribourg g, ..., fribourg gare]``;
* Prefixes of non-first words (``second_index``), ``[g, ga, gar, gare]``;
* Prefixes of individual words (``word_index``), ``[f, fr, fri, ..., fribourg, g, ga, gar, gare]``. This index handles word skips[^2].

Given the indexes, the search algorithm proceeds as follows:

1. Nearest locations (10km max distance) are searched for matches, first on ``second_index``, then on ``full_index``. The rationale behind this order is that most cities contain city name as the first word in the location name. Also, we limit this query by 1 result, since if you are searching for a local station - it is usually a specific one.
2. Search large-weight stations for matches on ``full_index``. Large-weight stations are big stations in the cities, such as ``Zurich HB`` or ``Geneva``.
4. Query for everything else using first ``full_index``, then ``second_index`` and finally ``word_index`` to handle word skips.

### Result analysis

After new search algorithm was deployed, we decided to analyze the changes in response times and user's typing patterns, e.g. if users now type less characters to search for locations.
The graphs for response times are presented below.

<figure style="width: 385px; margin-right: 25px;">
	<img alt="Geolocation XY response" src="/images/blog/2015-02-01-farplano-station-search/geolocation_response.svg" />
	<figcaption>Response times for retrieving top K stations closest to a given a (latitude, longitude) pair.</figcaption>
</figure>
<figure style="width: 385px;">
<img alt="Geolocation query response" src="/images/blog/2015-02-01-farplano-station-search/geolocation_query_response.svg" />
<figcaption>Response times for retrieving top K stations matching a given query + a (latitude, longitude) pair.</figcaption>
</figure>

As can be seen, both location- and query-based requests are now processed **~100ms faster** on average.

To perform the analysis of users' typing patterns, we have gathered the lengths of the search queries during a single search session that were followed by either a stationboard or a connection request (i.e. a user has completed his search task).
The distribution of lengths before and after deploying the new search algorithm are shown on the figure below:

<figure>
<img alt="Geolocation query length" src="/images/blog/2015-02-01-farplano-station-search/query_length.svg" />
<figcaption>Avg. query length: 8.09 (before)/7.32 (after). </figcaption>
</figure>

As can be seen from the distribution, after deploying new search algorithm which takes into account position of a user, the average search query length has decreased by a approximately one character.
Furthermore, now we can see that 3- and 4- length queries now constitute ~32% of all queries as compared to merely 22% before!

To conclude, by deploying the search algorithm locally, we have improved both the response time and users' satisfaction (by means of reducing query length).
We will continue monitoring the result and report updates on the search algorithm improvements.

[^1]: For example, the data provided by Swiss Federal Railways (SBB) can be found on [gtfs.geops.ch](http://gtfs.geops.ch/). Google also maintains a list of publicly available feeds on [code.google.com/p/.../PublicFeeds](https://code.google.com/p/googletransitdatafeed/wiki/PublicFeeds).
[^2]: For example, when searching for station ``Pont de Fayot``, user might start typing just ``Pont Fay..``.

