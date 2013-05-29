---
layout: post
title: "Ep.io django hosting"
date: 2012-01-08
comments: false
categories:
 - django
 - ep.io
 - en
 - gondor.io
 - prestashop-sync
 - hosting
---


<a href="https://www.ep.io/" imageanchor="1" style="margin-bottom: 1em; margin-right: 1em;"><img border="0" src="https://www.ep.io/static//images/logo.png" /></a>I've recently configured <a href="http://ep.io/">ep.io</a> python hosting (in my case - <b>django</b>) and found it to be really nice.
All configuration and deployment process took me about 2 hours and 50% of the time took writing of <a href="https://www.ep.io/docs/requirements/">requirements.txt</a> file describing my apps' dependencies.

Documentation on the site is very straightforward and clear, and there is a special deployment script that makes all process very handy. Moreover, <b>epio </b>supplies one dynamic app instance and celery process <a href="https://www.ep.io/pricing/">for free</a> (like on Google App Engine)!
Actually that was the feature that finally convinced me to choose <a href="http://ep.io/">ep.io</a> instead of <a href="https://gondor.io/pricing/">gondor.io</a> (On <b>gondor</b>, I need to pay 10$ for each slot, thus for 1 Django WSGI + PostgreSQL + Celery = 30$ per month at least).

So now you can find a copy of <a href="http://prestashop-sync.com/">Prestashop-Sync</a> on epio, at <a href="http://prestashop-sync.ep.io/">http://prestashop-sync.ep.io/</a>. It can be used if the main site is offline for some reason (but Databases there are not synced).
