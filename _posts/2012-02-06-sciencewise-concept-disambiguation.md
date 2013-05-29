---
layout: post
title: "ScienceWISE concept disambiguation interface"
date: 2012-02-06
comments: false
categories:
 - sciencewise
 - en
 - interface
---


Recently we did a new release of the ScienceWISE system, and one of the features introduced in this release is the interface for concept disambiguation. This interface is needed to handle the following problem: different scientific concepts can have the same <b>spelling</b>, especially acronyms. For example, <b>anomaly </b>in machine learning is not the same as anomaly in astrophysics or <a href="http://en.wikipedia.org/wiki/Anomaly">some other physics</a>, but in the scientific articles is can be names just as "anomaly".<br /><br />In all cases we're trying to do it automatically, but sometimes we don't have enough evidence to decide, and in this case we need a human to help us. And we made an interface resolve these ambiguites, and integrated it to both bookmarking and article annotation system. So here it is:<br /><br /><ul style="text-align: left;"><li>bookmarking interface: <a href="http://4.bp.blogspot.com/-0zZVbSBCk4M/Ty8mklupjpI/AAAAAAAADUY/3gM6uIOISKU/s1600/abbr1.png" imageanchor="1"><img border="0" src="http://4.bp.blogspot.com/-0zZVbSBCk4M/Ty8mklupjpI/AAAAAAAADUY/3gM6uIOISKU/s1600/abbr1.png" /></a></div></li><li>annotation interface: <a href="http://2.bp.blogspot.com/-LmVofE1AbQQ/Ty8mlkFfPzI/AAAAAAAADUc/S5jjveDTwzA/s1600/abbr2.png" imageanchor="1"><img border="0" height="347" src="http://2.bp.blogspot.com/-LmVofE1AbQQ/Ty8mlkFfPzI/AAAAAAAADUc/S5jjveDTwzA/s640/abbr2.png" width="640" /></a></div></li></ul><br />Later we will also try to use human-disambiguated data to improve our automatic concept detection.</div>
