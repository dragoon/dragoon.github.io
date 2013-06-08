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


Recently we did a new release of the ScienceWISE system,
and one of the features introduced in this release is the interface for concept disambiguation.
This interface is needed to handle the following problem: different scientific concepts can have the same **spelling**,
especially acronyms.
For example, **anomaly **in machine learning is not the same as anomaly in astrophysics or <a href="http://en.wikipedia.org/wiki/Anomaly">some other physics</a>,
but in scientific articles it can be named just as "anomaly".

In all cases we're trying to do it automatically, but sometimes we don't have enough evidence to decide,
thus we need a human to help us.
So we created an interface resolve these ambiguites, and integrated it to both bookmarking and article annotation system:

Bookmarking interface:

![](/images/blog/sw_abbr1.png)

Annotation interface:

![](/images/blog/sw_abbr2.png)

Later we will also try to use human-disambiguated data to improve our automatic concept detection.
