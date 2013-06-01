---
layout: post
title: "Django-celery the most terrible bug in my life"
date: 2012-03-01
comments: false
categories:
 - django
 - problem-solving
 - en
 - celery
---



<a href="http://proft.me/static/img/python/django_celery.png" imageanchor="1" style="clear: left; float: left; margin-bottom: 0.5em; margin-right: 1em;"><img border="0" src="http://proft.me/static/img/python/django_celery.png" /></a>This story began yesterday when I suddenly discovered that <a href="http://www.rabbitmq.com/">rabbitmq</a> (our message broker for celery) accumulated as many as **3184 (!!)** tasks that were wating to be executed.







I started investigation immediately and here is what I found at a first glance:
<ul style="text-align: left;"><li>Tasks were accumulated in the queue but* they did not finished*, tasks blocked all available workers and other tasks were just wating,</li><li>By examining the log files I found that this behavior had started recently after we did new system release.</li></ul>So, initially I tried to restart the celery and see if it works. As you can guess, it didn't. Then I did some investigations on another server and found an interesting thing: the* code inside the celery task was indeed executed, *but after *celery did not mark the task as completed*, so it got stuck in the queue forever blocking all the workers.

The things started to go beyond my comprehension. How it is even possible?? Why celery doesn't complete these tasks?
As a last resort, I started to do *code rollbacks* step by step on a development server, and eventually I found the commit that broke everything. The bad thing is that there was nothing wrong with this commit. Inside it was just a deletion of unused celery task! But the fact is that this commit breaks everything, so I made a rollback to latest working revision and started to perform code modifications, again step by step, restarting celery after each modification. **And I found the reason.**
Along with the deletion of unused task, the **import statement** of this task from another module was also removed. When I **inserted an import again**, everything started to work as expected, but the module did not use anything from this import!
So, I have successfully found the source of the problem and fixed it, but I still cannot explain such a weird behavior :(
