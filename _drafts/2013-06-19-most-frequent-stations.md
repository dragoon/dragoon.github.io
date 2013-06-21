---
layout: post
title: "Most freqent stations for the Stationboards app"
date: 2013-06-19
comments: false
categories:
- stationboards-app
- algorithms
- en
---

<img src="/images/blog/top_frequent stations.png" align="left">
In the lastest (3.4.6) version of the [Stationboards app](https://play.google.com/store/apps/details?id=com.schedulr)
we have introduced ability to pick two most frequent stations directly during the *geo-location phase*.

This is important because geo-location can sometimes take considerable amount of time, for many reasons.
And when this happened you had to manually type and search the desired station, which is annoying.
That's where we come to the question why we have put precisely **two most frequent stations**.
First reason is that something greater than two would probably look to heavy in the dialog window, and second,
most people still have two most frequent "natural" locations - home and office, and ability
to quickly pick any of them should be sufficient for the majority of cases (though we didn't perform any deep study on this).





