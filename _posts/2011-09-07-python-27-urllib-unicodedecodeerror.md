---
layout: post
title: "Python 2.7 urllib UnicodeDecodeError"
date: 2011-09-07
comments: false
categories:
 - urllib
 - httplib
 - python
 - bug
---


При обновлении ubuntu до<b> natty narwal</b>, и вместе с ней питона до версии <b>2.7</b>, наткнулся на баг (<a href="http://bugs.python.org/issue12398">http://bugs.python.org/issue12398</a>) в библиотеке <b>httplib</b>, которого небыло в <b>2.6</b> версии.<br /><br />Суть бага проста: когда производится http запрос с помощью функции <span style="font-size: small;"><span style="font-family: &quot;Courier New&quot;,Courier,monospace;">urllib2.urlopen</span></span>, при этом либо данные, либо url запроса являются строкой unicode, а также если url либо данные содержат<b> не только ascii-символы</b> то просходит ошибка с примерно таким трейсом:<br /><br /><pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; overflow: auto; padding: 5px;"> File "/usr/lib/python2.7/urllib2.py", line 126, in urlopen<br />   return _opener.open(url, data, timeout)<br /> File "/usr/lib/python2.7/urllib2.py", line 391, in open<br />   response = self._open(req, data)<br /> File "/usr/lib/python2.7/urllib2.py", line 409, in _open<br />   '_open', req)<br /> File "/usr/lib/python2.7/urllib2.py", line 369, in _call_chain<br />   result = func(*args)<br /> File "/usr/lib/python2.7/urllib2.py", line 1185, in http_open<br />   return self.do_open(httplib.HTTPConnection, req)<br /> File "/usr/lib/python2.7/urllib2.py", line 1154, in do_open<br />   h.request(req.get_method(), req.get_selector(), req.data, headers)<br /> File "/usr/lib/python2.7/httplib.py", line 955, in request<br />   self._send_request(method, url, body, headers)<br /> File "/usr/lib/python2.7/httplib.py", line 989, in _send_request<br />   self.endheaders(body)<br /> File "/usr/lib/python2.7/httplib.py", line 951, in endheaders<br />   self._send_output(message_body)<br /> File "/usr/lib/python2.7/httplib.py", line 809, in _send_output<br />   msg += message_body<br />UnicodeDecodeError: 'ascii' codec can't decode byte 0xd0 in position 5414: ordinal not in range(128)<br /></pre><br />Проблема, как можно заметить, случается при конкатенации строк, а они у нас в разной кодировке (В Python 2.6 видимо были какие-то дополнительные приведения к строкам). Таким образом чтобы исправить этот баг, необходимо вручную приводить url и данные к строковому виду, например с помощью<span style="font-family: &quot;Courier New&quot;,Courier,monospace;">url.encode('utf-8').</span>
