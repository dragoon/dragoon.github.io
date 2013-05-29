---
layout: post
title: "Как сделать rollback в Google App Engine"
date: 2011-08-29
comments: false
categories:
 - GAE
 - app engine
---


Иногда Google App Engine в процессе обновление код ломается и требует откатиться чтобы пойти дальше. Поиск правильного синтаксиса утомляет, поэтому сразу приведу его здесь:

<pre style="border: 1px dashed; margin: 0; padding: 5px;"><code>"C:\Program Files\Google\google_appengine\appcfg.py" -verbose \
--no_cookies --email=your_user@gmail.com --passin rollback .
</code></pre>
<code></code>Выполнять команду из каталога проекта.<h2>Comments</h2>


Roman Prokofyev
Писал в основном для себя, просто выполняете эту команду из каталога проекта, не забыв подставить свой email.
Олександр Тимченко
я не понял ничего
столкнулся с такой же проблемой
роскажите ,будьте любезны что делать пошагово,я днище девелоперское !
