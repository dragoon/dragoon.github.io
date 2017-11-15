---
layout: post
title: "Full-size poster visualizations of GTFS data"
date: 2017-11-16
comments: true
categories:
 - gtfs
 - visualization
 - public-transport
---

This post is a follow-up on my [previous effort]({% post_url 2017-05-06-gtfs-visualizations.md %}) of improving the tool for visualizing public transport routes (from GTFS data).
I wrote that I have added ability to restrict the map area by specifying the maximum allowed distance from the center.
The "distance-from-center" restriction was simple to implement and, by definition, it resulted in circular area restrictions.
This doesn't play well, however, with rectangular poster formats, and result in unused space.
Thus, I've improved implementation by computing bearing for each direction, and now area can by properly restricted with rectangular shapes.
A couple posters generated with this approach are here:

[Hamburg](/images/blog/2017-11-16-gtfs-visualizations-bearing/hvv.pdf)
[Berlin](/images/blog/2017-11-16-gtfs-visualizations-bearing/bvb.pdf)
[Saint-Petersburg](/images/blog/2017-11-16-gtfs-visualizations-bearing/spb.pdf)

The fork is located here:
[https://github.com/dragoon/gtfs-visualizations](https://github.com/dragoon/gtfs-visualizations)
