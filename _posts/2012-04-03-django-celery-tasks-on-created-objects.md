---
layout: post
title: "Django, celery tasks on created objects"
date: 2012-04-03
comments: false
categories:
 - django
 - en
 - celery
---


Sometimes, or may be quite often, you want to run an asynchronous task on the object after you create it.

For example, you want to populate some additional attributes, and this operation involves requests to external resources. Such requests, obviously, should be performed asynchronously, otherwise it is possible that you system will never respond to the request, waiting for external resources.

So you create a **<a href="http://celeryproject.org/">celery</a> **task ****for it, and that's it, right? NO!
By default, all requests in django are run *within a transaction*, therefore your celery task could start before the transaction is finished, and you get an **IntegrityError **on non-existing primary key or something similar.

There are a number of ways to solve this problem, and people are also discussing a possibility to add a <span style="font-family: 'Courier New', Courier, monospace;">on_tranaction_commit</span> signal to django: <a href="https://code.djangoproject.com/ticket/14051">https://code.djangoproject.com/ticket/14051</a>. This feature would definitely solve all the problems, but right now it even haven't passed decision phase.

The quick and dirty solution to fix is just to add a <span style="font-family: 'Courier New', Courier, monospace;">countdown</span><span style="font-family: inherit;"> attribute when running celery task:</span>
<a href="http://ask.github.com/celery/userguide/executing.html#eta-and-countdown">http://ask.github.com/celery/userguide/executing.html#eta-and-countdown</a>. This way the task will wait the specified amount of seconds and then start executing. The drawback is that it is really random, you just guess that *one minute*, for example, would be enough for the transaction to finish, but in fact it may be not.

The best way from perfectionist point of view to fix this would be to *commit transactions manually* after object creation or do some other semi-manual transaction management, but this appoach from my perspective could be *quite tedious and less error-prone*, so I will personally stick with the *quick and dirty* solution.
