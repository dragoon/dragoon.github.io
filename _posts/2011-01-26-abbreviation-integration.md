---
layout: post
title: "Abbreviation Integration"
date: 2011-01-26
comments: false
categories:
 - sciencewise
---

Наконец-то завершил интеграцию модуля расшифровки аббревиатур со стандартной системой обработки статей,
задача  заняла около недели работы, как всегда больше чем планировалось  изначально. Но теперь оно наконец-то работает, тесты написаны, уровень  правильной расшифровки аббревиатур научных понятий в статьях должен  заметно возрасти)
Вот как это выглядит сейчас:

<a href="http://3.bp.blogspot.com/-T7o_i8khTPk/ThgPZzYEIfI/AAAAAAAAC8s/P7IrFHeACv8/s1600/s640x480.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-T7o_i8khTPk/ThgPZzYEIfI/AAAAAAAAC8s/P7IrFHeACv8/s1600/s640x480.png" /></a>
Расшифровка  ошибочно попыталась угадать аббревиатуры  RP и NRP, но в данном случае  это является проблемой парсера TeX-исходника статьи, пропустившего  нужные места.
