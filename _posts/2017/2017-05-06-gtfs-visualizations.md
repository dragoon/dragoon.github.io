---
layout: post
title: "Visualizations of GTFS data"
date: 2017-05-06
comments: true
categories:
 - gtfs
 - visualization
---

Recently I came across a GitHub repo for visualizing GTFS data: [github.com/cmichi/gtfs-visualizations](https://github.com/cmichi/gtfs-visualizations)
(specifically public transport routes on the map).
The project looked very interesting and promising, so I wanted to apply it on my own GTFS datasets for Hamburg, Berlin and others.

Turned out there were several issues with the data processing scripts.
First, the code was not able to process large GTFS datasets.
Not only it loaded all GTFS files into memory (sometimes more than couple Gb), it also generated large intermediate shape files,
which [Processing](https://processing.org/) framework was not able to process and generate visualizations.

After several nights of work, I was able to address the large file issue by reworking the process of generating intermediate files.
The output now has a much smaller footprint, not larger than a ``shapes.txt`` file from the GTFS data.
I have also reworked the visualization code by iterating over the intermediate file instead of loading it completely into memory.

As extra perks, I've added some parametrization and a possibility to restrict the map area by specifying the maximum allowed distance from the center.

The fork is located here:
[https://github.com/dragoon/gtfs-visualizations](https://github.com/dragoon/gtfs-visualizations)

Here is the visualization of the public transport routes in the Hamburg urban area:
<img alt="Hamburg" src="/images/blog/2017-05-06-gtfs-visualizations/HVV.png" />


