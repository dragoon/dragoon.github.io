---
layout: post
title: "Django best practices resources, reusable apps with django"
date: 2012-12-06
comments: false
---


Few links on django best practices and on creating django reusable apps in particular:<br /><br /><a href="http://lincolnloop.com/django-best-practices/index.html">http://lincolnloop.com/django-best-practices/index.html</a><br /><a href="http://stackoverflow.com/questions/1419442/how-to-model-a-foreign-key-in-a-reusable-django-app">http://stackoverflow.com/questions/1419442/how-to-model-a-foreign-key-in-a-reusable-django-app</a><br /><br />The discussion on how to support multiple settings (first link) is especially interesting, because django doesn't give any clue on how to create such configurations.<br /><br />Personally I ended up using <b>dj-skeletor</b> app from github:&nbsp;<a href="https://github.com/senko/dj-skeletor">https://github.com/senko/dj-skeletor</a>, which basically has a special settings folder, one base settings file, and then specific setting files that import everything from base. To use either of them, you just symlink the right file to <b>local.py</b>.</div>
