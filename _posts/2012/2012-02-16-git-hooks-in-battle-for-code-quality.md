---
layout: post
title: "Git hooks in a battle for code quality"
date: 2012-02-16
comments: false
categories:
 - en
 - githooks
 - coding
 - git
---


<img src="/images/blog/githooks.jpg" align="left">
Almost every **VCS** has some sort of a hook system that developer can leverage. At work we use <a href="http://git-scm.org/">Git</a> and write on **Python**, and for such combination there is a great <a href="https://github.com/ablanco/githooks">githooks app</a> that allows to check commited files against pep8, pyflakes, pdb and jslint.

But honestly, I consider that rejecting *git push* just because of *pep8* or *pyflakes* *violations* to be *evil* for projects that did not follow these rules from the very beginning. For example, <a href="http://sciencewise.info/">ScienceWISE project</a> is one of those, and <a href="https://jenkins.shiningpanda.com/nltk/job/NLTK-py2.5/41/violations/">we're not alone</a>. The good thing is that now we constantly keep track of all violations inside <a href="http://jenkins-ci.org/">Jenkins</a> and we try to descrease their number with every commit.

But githooks is really useful when it comes to some *worst practices* checking, especially if these worst practices can be expressed as a *string or regex match*. So I decided to <a href="https://github.com/dragoon/githooks">fork githooks</a> and add my own custom checker. Here are the rules I have now:

{% highlight python %}
str_list = [('javascript:', 'Obtrusive javascript is forbidden'),
            ('HttpResponseNotFound', 'HttpResponseNotFound is forbidden, raise Http404 instead'),
            ('tasks.register\(', 'No need to register tasks anymore')]
re_list = [(re.compile(r'<.+onclick=.+>', re.I), 'Obtrusive javascript is forbidden (onclick)'),
           (re.compile(r'<.+style=.+>', re.I), 'Inline styles are forbidden'),
           (re.compile(r'\$\(.+#[^\s]+\)\.each'), 'Iteration on singleton elements is prohibited'),
           (re.compile(r'signals\..+?\.connect'), 'Old-style signals connect are forbidden, use @receiver'),
           (re.compile(r'class .+:\n(?!\s\s\s\s""")'), 'Not all classes have docstrings'),
           (re.compile(r'class .+?\((?:Periodic)?Task\):'), 'Old-style celery task classes are forbidden'),
           (re.compile(r'\.values_list\([^,]+(?!,flat=True)\)'), 'Didn\'t you forget to flatten quesryset?'),
           (re.compile(r'if\s?request\.method\s?==\s?'), 'Conditioning on request.method is forbidden, use decorators instead')]
{% endhighlight %}

As our team grows and people come and go, these simple heuristics should protect from doing really bad things, and I will try to extend and improve these lists while doing more and more code reviews :)

In future I would like to make these expressions in form of a django app, so anyone could add his custom rules.
