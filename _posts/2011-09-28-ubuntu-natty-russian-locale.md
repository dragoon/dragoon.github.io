---
layout: post
title: "Ubuntu natty russian locale"
date: 2011-09-28
comments: false
categories:
 - locale
 - ubuntu
---


Если после апрейда до **Ubuntu Natty** при установке новых пакетов появляется сообщение:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
 LANGUAGE = "en",
 LC_ALL = (unset),
 LANG = "ru_RU.utf8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").</pre>
То нужно сделать:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">aptitude install language-support-ru
</pre><h2>Comments</h2>


Anonymous
debian is true linux
