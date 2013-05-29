---
layout: post
title: "Pycharm local variable type declaration"
date: 2013-01-23
comments: false
categories:
 - pycharm
---


    Sometimes is it useful to make
        <b>PyCharm </b>know what type of variable you're using inside the function. For example, it
        enables the <i>auto-complete</i> feature for the variable methods and quick navigation
        to the method source with Ctrl/Cmd + click.



        While for the <i>function arguments</i> you can easily specify the type using the
            <i>docstring</i> notation like:
                <pre><code>
"""
:type arg1: list
:type arg2: dict
"""
(reStructured Text
            notation)
</code>
</pre>
        the documentation about such feature for local variables is buried in the <b>JetBrains</b>
        forum threads and issue tracker (<a href="http://youtrack.jetbrains.com/issue/PY-4083">http://youtrack.jetbrains.com/issue/PY-4083</a>).
        Here is the solution that worked for me:

        <pre><code>
var1 = a.object
""":type: MyModel"""
</code>
</pre>
        which means that <span style="font-family: inherit;"><i>var1</i></span> will be treated as
        <span style="font-family: inherit;"><i>MyModel</i></span> type.
