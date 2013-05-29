---
layout: post
title: "Memcached broken pipe issue"
date: 2011-11-03
comments: false
categories:
 - sciencewise
 - en
 - memcached
---


If you ever encounter the following message in <b>memcache </b>using set_multi/get_multi:

<span class="Apple-style-span" style="font-family: 'Courier New', Courier, monospace;">MemCached: MemCache: inet:127.0.0.1:11211: [Errno 32] Broken pipe.  Marking dead.</span>

or

<span class="Apple-style-span" style="font-family: 'Courier New', Courier, monospace;">Failed to write, and not due to blocking: Broken pipe</span>
<span class="Apple-style-span" style="font-family: 'Courier New', Courier, monospace;">
</span>
And if you're using <b>memcached 1.4.2</b> on ubuntu 10.04 LTS - then you need to upgrade to <b>memcached 1.4.5</b> from <b>Ubutnu Natty</b>.

Details: <a href="http://stackoverflow.com/questions/7980844/python-memcached-set-multi-storing-issue">http://stackoverflow.com/questions/7980844/python-memcached-set-multi-storing-issue</a>
