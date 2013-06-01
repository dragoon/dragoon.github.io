---
layout: post
title: "Git hooks in a battle for code quality"
date: 2012-02-16
comments: false
categories:
 - en
 - githooks
 - coding
---


<a href="http://4.bp.blogspot.com/-loP8yOjbpk0/T6TpnGtWJDI/AAAAAAAAD7s/FUoNURC1WxM/s1600/713-733-BLOODRED-HOOK.jpg" imageanchor="1" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="200" src="http://4.bp.blogspot.com/-loP8yOjbpk0/T6TpnGtWJDI/AAAAAAAAD7s/FUoNURC1WxM/s200/713-733-BLOODRED-HOOK.jpg" width="81" /></a>Almost every **VCS **has some sort of a hook system that developer can leverage. At work we use <a href="http://git-scm.org/">Git</a> and write on **Python**, and for such combination there is a great <a href="https://github.com/ablanco/githooks">githooks app</a> that allows to check commited files against pep8, pyflakes, pdb and jslint.

But honestly, I consider that rejecting *git push* just because of *pep8* or *pyflakes* *violations* to be *evil* ****for projects that did not follow these rules from the very beginning. For example, <a href="http://sciencewise.info/">ScienceWISE project</a> is one of those, and <a href="https://jenkins.shiningpanda.com/nltk/job/NLTK-py2.5/41/violations/">we're not alone</a>. The good thing is that now we constantly keep track of all violations inside <a href="http://jenkins-ci.org/">Jenkins</a> and we try to descrease their number with every commit.

But githooks is really useful when it comes to some *worst practices* checking, especially if these worst practices can be expressed as a *string or regex match*. So I decided to <a href="https://github.com/dragoon/githooks">fork githooks</a> and add my own custom checker. Here are the rules I have now:

<a href="http://1.bp.blogspot.com/-KVsxrr9e0RY/TzwiIacqrXI/AAAAAAAADUs/tzU3plQMbW8/s1600/githooks.png" imageanchor="1" style="clear: left; display: inline !important; margin-bottom: 1em; margin-right: 1em; text-align: center;"><img border="0" height="82" src="http://1.bp.blogspot.com/-KVsxrr9e0RY/TzwiIacqrXI/AAAAAAAADUs/tzU3plQMbW8/s640/githooks.png" width="640" /></a>
As our team grows and people come and go, these simple heuristics should protect from doing really bad things, and I will try to extend and improve these lists while doing more and more code reviews :)

In future I would like to make these expressions in form of a django app, so anyone could add his custom rules.
