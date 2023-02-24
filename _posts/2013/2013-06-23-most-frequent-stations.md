---
layout: post
title: "Most freqent stations for the Stationboards app"
date: 2013-06-23
comments: false
categories:
- stationboards-app
- algorithms
- en
---

<img src="/images/blog/top_frequent stations.png" align="left">
In the latest (3.4.6) version of the [Stationboards app](https://play.google.com/store/apps/details?id=com.schedulr)
we have introduced ability to pick two most frequent stations directly during the *geo-location phase*.

This is important because geo-location can sometimes take considerable amount of time, for many reasons.
And when this happened you had to manually type and search the desired station, which is annoying.
That's where we come to the question why we have put precisely **two most frequent stations**.
First reason is that something greater than two will probably start to look too heavy in the dialog window, and second,
most people still have two most frequent "natural" locations - *home and office*, and ability
to quickly pick any of them should be sufficient for the majority of cases (though we didn't perform any deep study on this).

I would like to also go through some implementation details. Initially it's very straightforward.
Each time a user loads some station, the app either adds this station to the database with a count of one,
or increments the station's count if already exists.
But there are two hidden pitfalls here &mdash; unlimited increments for both number of usages per station and the overall count of stations itself.

The number of usages per station is important not because of potential integer/long overflow.
Nowadays, it's more likely that the end of the world will happen earlier than someone will access some station 2<sup>64</sup> times during his life.
This number is important because it's very likely that a person can **change his home/office many times**.
So we want to set some kind of limit on the maximum value this number can take,
and this value should decrease when a person changes his home/office location.
At the moment I've only implemented the limit, but I also plan to add some value decrement mechanism,
so the app will be able to adapt to new home/office locations.

The total amount of stations in the database is important just because we don't want to slow down things where it's not necessary.
SQLite database in Android is quite slow, and for our purposes there is no need to keep all the stations a person ever visited.
Thus every time the total number of stations in the table exceeds certain limit, the app deletes rarely used stations up to this limit.
To avoid constant database deletions, we have implemented a simple threshold algorithm that allows the total number of stations
in the table grow to a certain number *N*, and after reaching this number the app deletes all the stations up to a different number *M < N*.





