---
layout: post
title: "Ubuntu natty russian locale"
date: 2011-09-28
comments: false
categories:
 - locale
 - ubuntu
---


Если после апрейда до <b>Ubuntu Natty</b> при установке новых пакетов появляется сообщение:<br /><pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">perl: warning: Setting locale failed.<br />perl: warning: Please check that your locale settings:<br />&nbsp;LANGUAGE = "en",<br />&nbsp;LC_ALL = (unset),<br />&nbsp;LANG = "ru_RU.utf8"<br />&nbsp;&nbsp;&nbsp; are supported and installed on your system.<br />perl: warning: Falling back to the standard locale ("C").</pre><br />То нужно сделать: <br /><pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">aptitude install language-support-ru<br /></pre><h2>Comments</h2>


Anonymous
debian is true linux
