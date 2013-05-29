---
layout: post
title: "New PrestaShop-Sync, how it was made"
date: 2011-09-16
comments: false
categories:
 - en
 - prestashop-sync
---


It's been more than six months since we launched <a href="http://prestashop-sync.com/">prestashop-sync.com</a>. (Despite the fact that the domain was registered only on the 27th of May, before that the service had run on <b>Google App Engine</b> domain, prestashop-sync.appspot.com)

Throughout this time, we gradually, step by step, tried to make the service better and get rid of various bugs discovered by our kind users.

Initially, the service did not possess any design, development was chaotic, interface accumulated more and more new elements but the old ones did not intend to leave.

You can see this initial version of the service interface on the screenshot below:
<a href="http://3.bp.blogspot.com/-5m5bzjzIdBs/TnMTA7Fu6yI/AAAAAAAADB0/mDWYxfmgwQQ/s1600/old.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="640" src="http://3.bp.blogspot.com/-5m5bzjzIdBs/TnMTA7Fu6yI/AAAAAAAADB0/mDWYxfmgwQQ/s640/old.png" width="582" /></a>

Yes, it doesn't look very ugly, but it definitely has shortcomings.
The interface was made from ordinary rectangular blocks (albeit with rounded corners), the same buttons, plus some other stuff, "successfully" borrowed from other sites. And the most terrible was non-attractive look site color theme - shades of gray. The site has slowly began to turn into a mess, and therefore it was decided to develop a new design from scratch, but try to preserve and improve the original service workflow at the same time.

We have invited a web designer, described him the purpose of the service, its functionality, showed him sites that we like, and asked for a couple of sketches.
The first attempt, as usual, came out lumpy (only on russian, sorry for that:)):

<a href="http://2.bp.blogspot.com/-D2fZ-PnVsXs/Tm4btYTIiYI/AAAAAAAADAg/5hCHSnVWy9Q/s1600/site_template_v1b.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-D2fZ-PnVsXs/Tm4btYTIiYI/AAAAAAAADAg/5hCHSnVWy9Q/s1600/site_template_v1b.png" /></a>

I forgot to tell the designer that we want to see the interface in the original <a href="http://prestashop.com/">PrestaShop.com</a> color scheme, moreover the overall impression on this sketch was quite ambiguous, so we continued to work on the design.

The second one appeared much better and we decided to give it a try:
<a href="http://3.bp.blogspot.com/-qFpSz-PbIqw/TnMOFk8MXTI/AAAAAAAADBg/OHxzKzNANlM/s1600/service.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="640" src="http://3.bp.blogspot.com/-qFpSz-PbIqw/TnMOFk8MXTI/AAAAAAAADBg/OHxzKzNANlM/s640/service.png" width="555" /></a>

Then we continued to work on details to make the service as far as possible convenient and understandable for our users.

Now I'll dwell on the various features of the new interface and show how it differs from the old one:
<ol><li><b>PrestaShop </b>color scheme<b>. </b>
I've already mentioned this earlier, now in detail: we decided to get rid of gray shades dominance and make something more bright, so we considered the PrestaShop color scheme and found it to be quite good and reasonable, because it gives the impression of some relation between our service and PrestaShop.</li><li><b>Service feature block</b>:
<a href="http://1.bp.blogspot.com/-IXXLyKOHWMM/TnMMU-bosdI/AAAAAAAADBc/SezxZxKIzKg/s1600/adv.png" imageanchor="1"><img border="0" src="http://1.bp.blogspot.com/-IXXLyKOHWMM/TnMMU-bosdI/AAAAAAAADBc/SezxZxKIzKg/s1600/adv.png" /></a>
In this block we have introduced a possibility to dynamically change slides to accommodate several paragraphs of text. Also, to not bother our users that have already read it, we have added a button to collapse block into a small semi-transparent line. Moreover, the state of the block will persist across visits so users don't have to collapse it again.</li><li><b>Navigation help steps right besides functional blocks.</b>
Help on how to use service had already present in the first service incarnation, but first, its placement wasn't perfect at all, and second, we couldn't put any reasonable text in the space allotted for it. So we had split this block into smaller pieces and added corresponding descriptions to each functional block in the new version. We have also added numbers on these blocks to explicitly define the sequence to follow:
<a href="http://1.bp.blogspot.com/-Zni15OFdUeg/TnMOiAwJl6I/AAAAAAAADBk/BfuebhoaXXA/s1600/help.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://1.bp.blogspot.com/-Zni15OFdUeg/TnMOiAwJl6I/AAAAAAAADBk/BfuebhoaXXA/s1600/help.png" /></a>
</li><li><b>New update product quantity button.</b>
In the previous service version the indicator of upgrade process for a particular product was made in the form of a rotating element next to the "<b>update</b>" button:

<a href="http://2.bp.blogspot.com/-WjqzV9kQHN4/TnMToTmSxxI/AAAAAAAADB4/phc4JMZyGtk/s1600/1update.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-WjqzV9kQHN4/TnMToTmSxxI/AAAAAAAADB4/phc4JMZyGtk/s1600/1update.png" /></a><a href="http://4.bp.blogspot.com/-zsCmEWOyzcw/TnMTuG4AChI/AAAAAAAADB8/6czedJFPYjA/s1600/2update.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://4.bp.blogspot.com/-zsCmEWOyzcw/TnMTuG4AChI/AAAAAAAADB8/6czedJFPYjA/s1600/2update.png" /></a>
In the new version we have gone further - because the button is not needed until the update is finished, we have combined these elements. The result turned out to be nice and easy:

<a href="http://3.bp.blogspot.com/-kn8xm9ri9jk/Tm47f-ZM04I/AAAAAAAADAo/HxXCoKv4ePY/s1600/loader2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-kn8xm9ri9jk/Tm47f-ZM04I/AAAAAAAADAo/HxXCoKv4ePY/s1600/loader2.png" /></a><a href="http://1.bp.blogspot.com/-He7ht5ZzPkk/Tm47gMu2kNI/AAAAAAAADAs/VY3tpD5iZmA/s1600/ok2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://1.bp.blogspot.com/-He7ht5ZzPkk/Tm47gMu2kNI/AAAAAAAADAs/VY3tpD5iZmA/s1600/ok2.png" /></a>
</li><li>Every shop is a shop list has its <b>status indicator</b>: <b>green </b>- means everything is ok and you can work with the shop, <b>red </b>- the error has occurred and you can't work with the shop right now. Previously, we had a separate status update button  in a column called "<b>actions</b>". But why do we need a separate button to update the status if it is possible to merge then into one element?

Thus we have reduced the diversity of different actions and indicators while keeping the ease of use: <a href="http://3.bp.blogspot.com/-xFK4D33iMWQ/TnMP3NaZwwI/AAAAAAAADBs/TquDeM0EghE/s1600/actions.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-xFK4D33iMWQ/TnMP3NaZwwI/AAAAAAAADBs/TquDeM0EghE/s1600/actions.png" /></a>
</li><li><b>Trapezoid buttons.</b>
Another our innovation - non-standard buttons in the shape of a trapezoid. Implementation of this element was one of the most difficult tasks, but they look very impressive:
<a href="http://1.bp.blogspot.com/-ZRNB3WS4EsM/TnMPWMFOTPI/AAAAAAAADBo/p1u0ZQIrW0c/s1600/buttons.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://1.bp.blogspot.com/-ZRNB3WS4EsM/TnMPWMFOTPI/AAAAAAAADBo/p1u0ZQIrW0c/s1600/buttons.png" /></a>
</li><li><b>Article count.</b>
The idea is pretty simple - to let our visitors immediately see the number of articles on our site. While the number of articles is not very large - it may be quite reasonable:
<a href="http://1.bp.blogspot.com/-6HUZO_3e4Rc/TnMSeD6MWLI/AAAAAAAADBw/XzGkcQKyVXQ/s1600/articles.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://1.bp.blogspot.com/-6HUZO_3e4Rc/TnMSeD6MWLI/AAAAAAAADBw/XzGkcQKyVXQ/s1600/articles.png" /></a></li></ol>
