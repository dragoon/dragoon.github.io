---
layout: post
title: "Linking PyCharm with an Issue Tracker"
date: 2012-01-26
comments: false
categories:
 - ide
 - en
 - pycharm
---


<a href="http://3.bp.blogspot.com/-ex8sfbybYF4/Tx83ODk-o_I/AAAAAAAADUA/y_OaWMHTpKw/s1600/header_pycharm20.png" imageanchor="1" style="margin-bottom: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-ex8sfbybYF4/Tx83ODk-o_I/AAAAAAAADUA/y_OaWMHTpKw/s1600/header_pycharm20.png" /></a>

I fell in love with <a href="http://www.jetbrains.com/pycharm/">PyCharm</a> since 2010 when it was first announced, and even earlier I was a big fan of
<a href="http://www.jetbrains.com/idea/">Intellij IDEA</a> IDE for Java. Actually I think all JetBrains IDEs are first-class products, because they are built on the same platform.

So that was an introduction, and in this post I'd like show how to configure <a href="http://www.jetbrains.com/pycharm/webhelp/issue-navigation.html">Issue Navigation in PyCharm</a>, because as you may see, official documentation just gives some bare description to the fields.

At work we're using super nice <a href="http://www.redmine.org/">Redmine</a> tracker, and here is the issue navigation pattern for it:

**Issue ID:** <span style="font-family: 'Courier New', Courier, monospace;">#(\d+)</span>
**Issue Link:** <span style="font-family: 'Courier New', Courier, monospace;">http://redmine.<i>yoursite.com</i>/issues/$1</span>

For my personal projects I prefer <a href="https://bitbucket.org/">bitbucket</a>, because it gives you private repositories for free, of course:
**Issue ID:** <span style="font-family: 'Courier New', Courier, monospace;">#(\d+)</span>
**Issue Link:** <span style="font-family: 'Courier New', Courier, monospace;">https://bitbucket.org/<i>username</i>/prestashop-sync/issue/$1</span>

As you may see, this configuration is really simple, and other issue tracking systems can be linked easily based on my examples.

In the end you should see commit history with hyperlinks to the issues:
<a href="http://4.bp.blogspot.com/-467_frlJeM8/TyBi8myNC3I/AAAAAAAADUI/BSmcoVzqNGw/s1600/history.png" imageanchor="1" style="margin-bottom: 1em; margin-right: 1em;"><img border="0" height="158" src="http://4.bp.blogspot.com/-467_frlJeM8/TyBi8myNC3I/AAAAAAAADUI/BSmcoVzqNGw/s640/history.png" width="640" /></a>

