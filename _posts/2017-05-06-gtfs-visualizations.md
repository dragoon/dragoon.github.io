---
layout: post
title: "Visualizations of GTFS data"
date: 2017-05-06
comments: true
categories:
 - gtfs
 - visualization
---

Recently I came across a GitHub repo for visualizing GTFS data: [github.com/cmichi/gtfs-visualizations](https://github.com/cmichi/gtfs-visualizations). The project looked very interesting and promising, and I wanted to apply it on my own GTFS datasets of Hamburg, Berlin, etc. It turned out there were several issues.

However, the code was not able to process large GTFS dataset, not only it loaded GTFS files themselves into memory, it also generated large intermediate shape files, which (Processing)[https://processing.org/] framework was not able to process and generate visualizations.

After several nights of work, I was able to address the large file issue by reworking the process of generating intermediate files. The output now has a small footprint not much larger than a ``shapes.txt`` file from the GTFS source. I have also reworked the visualization code by iterating over the intermediate file instead of loading it again completely into memory.
Then I added some parametrization to the script and a possibility to restrict the visualization area by specifying the maximum allowed distance from the center.

The fork is located here:
[https://github.com/dragoon/gtfs-visualizations](https://github.com/dragoon/gtfs-visualizations)

Here is the visualization of the public transport routes in the Hamburg urban area:
<img alt="Hamburg" src="/images/blog/2017-05-06-gtfs-visualizations/HVV.png" />


