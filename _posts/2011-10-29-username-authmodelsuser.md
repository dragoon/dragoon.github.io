---
layout: post
title: "Поле username в модели auth.models.User"
date: 2011-10-29
comments: false
categories:
 - django-auth
 - django
 - django-models
---


При наследовании стандартной модели пользователя в <b>Django </b>одной из частых проблем является соблюдение ограничений, наложенных этой моделью.<br /><br />Например, поле <b>username </b>является обязательным и должно содержать не более 30 символов. Вполне нормальное ограничение, но чем заполнять это поле если в системе <b>вместо логина используется email</b>?<br />Решение, которое мы недавно начали использовать в нашем проекте - задание полю&nbsp;<b>username</b>&nbsp;значения <b>primary key</b> (pk),&nbsp;приведенного&nbsp;к строке. Очень просто в реализации и 30-ти символов в данном случае будет более чем достаточно даже для крупного проекта.</div><h2>Comments</h2>


perython
Спасибо за ответ!<br /><br />Да, ваше решение выглядит красивее. Как же сам не догадался)
Roman Prokofyev
Без переопределения никак если вы хотите наследоваться от модели django, а не делать собственную. <br />Мы сделали почти так как вы, только не делаем повторного сохранения модели, не очень понятен смысл этого. Просто переопределяем метод save() у наследуемой модели:<br /><br />def save(self, *args, **kwargs):<br />   ...<br />   self.username = str(self.id)<br />   ...<br />   super(Profile, self).save(*args, **kwargs)
perython
Здравствуйте!<br /><br />Тоже делаю авторизацию по email.<br />написал так:<br /><br />...<br />newuser = UserProfile(<br />    username=&#39;just-because-it-is-required&#39;,<br />    email=cd[&#39;email&#39;]<br />)<br />newuser.set_password(cd[&#39;password&#39;])<br />newuser.save()<br /><br />newuser.username = str(newuser.pk)<br />newuser.save()<br />...<br /><br />Т.е. без переопределения username никак не обойтись?<br />А вы как запрогали?
