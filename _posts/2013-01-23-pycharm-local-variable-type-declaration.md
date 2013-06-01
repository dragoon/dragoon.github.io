---
layout: post
title: "Pycharm local variable type declaration"
date: 2013-01-23
comments: false
categories:
 - pycharm
 - en
---

Sometimes is it useful to make **PyCharm **know what type of variable you're using inside the function.
For example, it enables the *auto-complete* feature for the variable methods and quick navigation
to the method source with Ctrl/Cmd&nbsp;+&nbsp;click.

While for the *function arguments* you can easily specify the type using the
*docstring* notation like:
{% highlight python %}
# (reStructured Text notation)
"""
:type arg1: list
:type arg2: dict
"""
{% endhighlight%}
the documentation about such feature for local variables is buried in the **JetBrains**
forum threads and issue tracker (<a href="http://youtrack.jetbrains.com/issue/PY-4083">http://youtrack.jetbrains.com/issue/PY-4083</a>).
Here is the solution that worked for me:
{% highlight python %}
var1 = a.object
""":type: MyModel"""
{% endhighlight%}
which means that *var1* will be treated as *MyModel* type.
