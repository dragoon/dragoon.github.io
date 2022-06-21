---
layout: post
title: "Error handling in ScienceWISE"
date: 2011-12-01
comments: false
categories:
 - sciencewise
 - en
---


A lot of scientific projects suck when it comes to user interfaces.
I think this usually happens because they can't just hire professional designers and usability experts, and project managers,
they should do **a lot of science**, conduct experiments, obtain data, you know, and such irregularity leads to ugly interfaces, if any.

Here, at **<a href="http://sciencewise.info/">ScienceWISE</a>**, we also can't hire professional designers ;), but we always try to make the most of our abilities, try to make the project look attractive and make our visitors feel comfortable using it.

Soon we will be releasing a lot of small visual interface improvements, and here I would like to take a look at one of them, because it is somewhat an nonstandard decision.

So, here we have our main page, and now let's try to process article with some bad ID:

<a href="http://1.bp.blogspot.com/-saUxErwthBk/TtdCMH5JTYI/AAAAAAAADFU/VJ8XpmcWGwg/s1600/Screen+shot+2011-12-01+at+9.58.53+.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="115" src="http://1.bp.blogspot.com/-saUxErwthBk/TtdCMH5JTYI/AAAAAAAADFU/VJ8XpmcWGwg/s640/Screen+shot+2011-12-01+at+9.58.53+.png" width="640" /></a>
<a href="http://3.bp.blogspot.com/-74hFyTC8u_4/TtdCMkcHXGI/AAAAAAAADFY/l2SmEMvlHUc/s1600/Screen+shot+2011-12-01+at+9.59.10+.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="116" src="http://3.bp.blogspot.com/-74hFyTC8u_4/TtdCMkcHXGI/AAAAAAAADFY/l2SmEMvlHUc/s640/Screen+shot+2011-12-01+at+9.59.10+.png" width="640" /></a>
<a href="http://4.bp.blogspot.com/--DiQSo-KS_Y/TtdCNISBkcI/AAAAAAAADFk/4ybd9sM796A/s1600/Screen+shot+2011-12-01+at+9.59.28+.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="118" src="http://4.bp.blogspot.com/--DiQSo-KS_Y/TtdCNISBkcI/AAAAAAAADFk/4ybd9sM796A/s640/Screen+shot+2011-12-01+at+9.59.28+.png" width="640" /></a>

Here, we have an error that is shown in the same field as a watermark text.
The error will disappear when we try to enter another article ID. 
This way we save screen space comparing to the standard way of showing errors separate near input fields.
