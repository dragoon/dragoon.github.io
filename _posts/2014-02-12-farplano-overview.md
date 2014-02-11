---
layout: post
title: "Farplano: overview"
date: 2014-02-14
comments: false
categories:
- stationboards-app
- en
---
<img src="https://lh4.ggpht.com/BUloY6vAaP6hTGvpN_8ASWJFEW2trFg28aPIy5iBDr407W6_18IJUbgHIKgEakX5Jw=w300-rw">
This note is going to prelude a series of posts aimed to expose architectural and design decisions
of the former *Swiss Stationboards* app.

First of all, let me briefly summarize few things that happened since the last update on the topic:

1. The app was renamed to *Faplano* and received a brand new logo for better
recognition and memorability among other transportation apps (thanks to great 99designs).
2. We've added the calendar journey planning feature
which automatically plans a journey from user's current location to
some destination specified as a location attribute of a calendar event.
This feature is available as a paid subscription at the moment and
this is one thing I'm going write about the upcoming posts.

Moving forward, here is the preliminary set of topics for the next posts:

1. Merging lines with the same number but different destinations (route retrieval, checking if schedules interleave, checking next station after current one, using a set vs. last destination variable, problem at terminal stations)
2. Calendar journey planner (flights, skips for close connections, viewpager and dynamic loader mechanism, connections back, journey caching)
3. Automatic stationboard updates. (use case: removing manual update button, when to update? saving last update time, canceling timer to prevent unwanted network I/O)
4. Route prediction (not yet implemented).

