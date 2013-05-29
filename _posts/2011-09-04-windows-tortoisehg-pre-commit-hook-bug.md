---
layout: post
title: "Windows TortoiseHg pre-commit hook bug"
date: 2011-09-04
comments: false
categories:
 - mercurial
 - hook
 - bug
 - hghooks
 - hg
 - tortoisehg
---


Пост о баге, с которым можно столкнуться при настройке хуков в **mercurial**, работая с клиентом <a href="http://tortoisehg.bitbucket.org/">TortoiseHg</a> под Windows.

Итак, я настраивал хуки в **mercurial** для автоматической проверки python-кода с помощью пакета <a href="http://pypi.python.org/pypi/hghooks/">hghooks</a>. Данный пакет содержит готовые хуки для провеки кода на соответствие PEP8 и с помощью анализатора <a href="http://pypi.python.org/pypi/pyflakes">pyflakes</a>.

В документации предлагается просто добавить к конфиг **mercurial** (hgrc, mercurial.ini) следующие строки:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">[hooks]
pretxncommit.pep8 = python:hghooks.code.pep8hook
pretxncommit.pyflakes = python:hghooks.code.pyflakeshook
pretxncommit.pdb = python:hghooks.code.pdbhook</pre><pre></pre>
Однако в моём случае после этой настройки комит вылетел с ошибкой вида:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">abort: pretxncommit.pep8 hook is invalid (import of "hghooks.code" failed)</pre><pre></pre>
Дело в том, что клиент **TortoiseHg ** не умеет использовать никакие установленные библиотеки кроме тех из файла **library.zip**, расположенного по умолчанию в **c:\Program Files\TortoiseHg\**. Поэтому для устранения ошибки надо добавить в архив каталоги **hghooks**, **pyflakes **и файл **pep8.py**.
