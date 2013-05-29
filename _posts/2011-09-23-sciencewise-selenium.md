---
layout: post
title: "Django Selenium integration"
date: 2011-09-23
comments: false
categories:
 - sciencewise
 - django
 - selenium
---


Давным-давно в нашем научном проекте <a href="http://sciencewise.info/">ScienceWISE</a> был написан код для возможности запуска <a href="http://seleniumhq.org/">Selenium</a> тестов, позволяющих тестировать взаимодействие пользователя с приложением.

Во время написания кода о модульности и слабом связывании никто не думал, поэтому код оказался сильно завязан на другие части приложения ScienceWISE, а большинство констант были что называется <b>hard-coded</b>.

И вот сейчас мы наконец-то выделили интеграцию Django и Selenium в отдельное приложение, встречаем:<a href="https://github.com/dragoon/django-selenium"> https://github.com/dragoon/django-selenium</a>, также на PyPi: <a href="http://pypi.python.org/pypi/django-selenium">http://pypi.python.org/pypi/django-selenium</a>.
Более подробное описание: <a href=""></a><a href="http://habrahabr.ru/blogs/django/129107/">http://habrahabr.ru/blogs/django/129107/</a>

