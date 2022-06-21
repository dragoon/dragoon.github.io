---
layout: post
title: "Вопросы для собеседования по python/django"
date: 2011-11-23
categories:
 - собеседование
 - python
---


Сборники вопросов на собеседовании по python/django + немного моих собственных
* <a href="http://pyobject.ru/blog/2010/02/04/python-quiz/">http://pyobject.ru/blog/2010/02/04/python-quiz/</a>
* <a href="http://zxmd.wordpress.com/2010/11/23/python_interview_questions/">http://zxmd.wordpress.com/2010/11/23/python_interview_questions/</a>
* <a href="http://habrahabr.ru/qa/5269/">http://habrahabr.ru/qa/5269/</a>
* <a href="http://agiliq.com/blog/2009/12/django-quiz/">http://agiliq.com/blog/2009/12/django-quiz/</a>
* Есть набор данных, над которым требуется выполнять операции проверки на вхождение заданного элемента в набор. Какую структуру данных лучше всего использовать для хранения набора и почему? (set, dict)
* Вопрос про оптимизацию кода при вызове метода класса(именно класса а не экземпляра класса) (сохранить в локальную переменную)
* Где в django используется паттерн observer (наблюдатель)? (signals)
* Где в django используются <a href="http://docs.python.org/howto/descriptor.html">дескрипторы</a> и для каких целей? (model managers, foreign keys, request.user auth, form.errors)
* Model manager (<strong>django.db.models.manager.ManagerDescriptor</strong>) дескриптор служит только для того, чтобы атрибут objects нельзя было получить у экземпляра модели, только у класса.
* Foreign keys (<strong>django.models.fields.related.ReverseSingleRelatedObjectDescriptor)</strong> - получает объект модели, отвечающий Foreign Key и кэширует его.
* Как в django сделать эффективный по памяти и по скорости цикл по большому объёму записей в базе, если это возможно? (queryset.iterator())
* Jquery - Как глобально запретить все хэндлеры на элементах которые отвечают определённому условию? (например имеют  class=disabled, а также запретить действия по умолчанию), <a href="http://stackoverflow.com/questions/7864978/jquery-ignore-elements-with-disabled-class" id="" shape="rect" style="text-align: -webkit-auto;" target="_blank">http://stackoverflow.com/questions/7864978/jquery-ignore-elements-with-disabled-class</a>
Конечно, сам я сходу не отвечу и на половину :)
