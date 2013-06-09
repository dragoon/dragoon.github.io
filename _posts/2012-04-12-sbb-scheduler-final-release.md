---
layout: post
title: "Swiss Stationboards stable release (Obsolete)"
date: 2012-04-12
comments: false
categories:
 - en
 - stationboards-app
---


It's been some time since <a href="http://prokofyev.ch/2012/03/tpf-mobile-app.html">I wrote about TPF Scheduler</a>. In the meanwhile, I've attended <a href="http://make.opendata.ch/doku.php?id=event:2012-03">second Swiss OpenData Camp</a> in Geneva with the hope to find information about *Swiss Public Transport API*. And I found it! The API was shown to the public on this event and now anyone can query public transport API (or install by yourself) located at: <a href="http://transport.opendata.ch/">http://transport.opendata.ch/</a>.

This API was exactly what I need to finish my application. So after a week of work I've upgraded my TPF application to work with this API and support *all public transport* across Switzerland.

As usual, application can be access from the same url: <a href="http://prokofyev.ch/tpf/">http://prokofyev.ch/tpf/</a> and also from <a href="http://prokofyev.ch/sbb/">http://prokofyev.ch/sbb/</a>.
I've also added HTML5 **geolocation **to it, so if you're inside Switzerland, you can try it and see what station are near you. If you're not, there is also a possibility to supply raw coordinates:
<br>
<a href="http://prokofyev.ch/sbb/?x=46.802877773762894&amp;y=7.151651249648352">http://prokofyev.ch/sbb/?x=46.802877773762894&amp;y=7.151651249648352</a>.

Current features of the application include:

* Automatic geolocation and finding nearest stations
* Buttons to update location and to update schedule for the current station
* Filtration of stations by train-only stations.

Description of the project on the make.opendata.ch: <a href="http://make.opendata.ch/doku.php?id=project:transport:swiss-scheduler">http://make.opendata.ch/doku.php?id=project:transport:swiss-scheduler</a>

Here are the final screenshots:

<a href="http://4.bp.blogspot.com/-yMRhCo-bXO4/T4XnoNmDI_I/AAAAAAAADro/HZUL0-N8hSo/s1600/screenshot1.png" imageanchor="1" style="float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="400" src="http://4.bp.blogspot.com/-yMRhCo-bXO4/T4XnoNmDI_I/AAAAAAAADro/HZUL0-N8hSo/s400/screenshot1.png" width="246" /></a><a href="http://4.bp.blogspot.com/-TRXakuFaW8o/T4XnpPNNHNI/AAAAAAAADrw/4FyT_mkRl0Y/s1600/screenshot2.png" imageanchor="1" style="float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="400" src="http://4.bp.blogspot.com/-TRXakuFaW8o/T4XnpPNNHNI/AAAAAAAADrw/4FyT_mkRl0Y/s400/screenshot2.png" width="253" /></a><a href="http://3.bp.blogspot.com/-IBo5kz-E9Hk/T4XnqJ889OI/AAAAAAAADr4/Dk4SO--l0Lo/s1600/screenshot3.png" imageanchor="1" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="400" src="http://3.bp.blogspot.com/-IBo5kz-E9Hk/T4XnqJ889OI/AAAAAAAADr4/Dk4SO--l0Lo/s400/screenshot3.png" width="262" /></a>


