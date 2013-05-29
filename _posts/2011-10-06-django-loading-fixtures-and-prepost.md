---
layout: post
title: "Django loading fixtures and pre/post save signals"
date: 2011-10-06
comments: false
categories:
 - django-signals
 - django
---


Recently I was trying to restore tests for Django application. After doing some refactoring, I encountered a new error that had happened in every test during fixture loading:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">Problem installing fixture 'articles_data.json': Traceback:
  File ".../django/core/management/commands/loaddata.py", line 172, in handle
    obj.save(using=using)
  File ".../django/core/serializers/base.py", line 165, in save
    models.Model.save_base(self.object, using=using, raw=True)
  File ".../django/db/models/base.py", line 500, in save_base
    rows = manager.using(using).filter(pk=pk_val)._update(values)
  File ".../django/db/models/query.py", line 491, in _update
    return query.get_compiler(self.db).execute_sql(None)
...
IntegrityError: (1062, "Duplicate entry 'cwdm.tex' for key 'literal_id'")
</pre>
Also, a lot of tests just didn't pass.

After doing some research I found that the problem is related to the newly created **<a href="https://docs.djangoproject.com/en/dev/topics/signals/">signals code</a>** attached to my models.

In fact, when django **loads fixtures** for your application, it also **implicitly executes all signals** attached to the models, not just plain database population, and this behavior may seem somewhat odd. There is a a ticket about that in django tracker (<a href="https://code.djangoproject.com/ticket/12610">https://code.djangoproject.com/ticket/12610</a>), but the future of this ticket is undecided yet.

So right now you can use undocumented <i>'raw' </i>parameter in the **signal function** to suppress such behavior if required:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">def my_signal(sender, instance, created, **kwargs):
    if kwargs.get('raw'):
        return
    ....
models.signals.post_save.connect(my_signal, sender=MyModel)
</pre>
<i>'raw' parameter</i> is used in django internals, and it equals <i>True</i> when the fixture is loaded.
