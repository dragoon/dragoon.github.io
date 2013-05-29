---
layout: post
title: "Баг в AD Connector для Oracle Identity Manager"
date: 2011-07-13
comments: false
categories:
 - юмор
 - bug
 - Oracle
---


See short English version below.
Сегодня наконец-то закончилась недельная эпопея борьбы с OIM, в итоге удалось успешно подсоединиться к Active Directory, но это неважно. Важно то, что в процессе поиска неисправностей я дошёл до декомпиляции кода коннектора Oracle, приведу здесь небольшой сниппет:

<pre style="background-image: URL(http://2.bp.blogspot.com/_z5ltvMQPaa8/SjJXr_U2YBI/AAAAAAAAAAM/46OqEP32CJ8/s320/codebg.gif); background: #f0f0f0; border: 1px dashed #CCCCCC; color: black; font-family: arial; font-size: 12px; height: auto; line-height: 20px; overflow: auto; padding: 0px; text-align: left; width: 99%;"><code style="color: black; word-wrap: normal;">   if(i &lt;= as.length)
     break;
   if(as[i].equalsIgnoreCase("IT Resource.Key"))
   {
     l = tcresultset.getLongValue(as[i]);
     break;
   }
</code></pre>
Обратите внимание на вшитую константу - "IT Resource.Key", которая есть не что иное, как название столбца в базе данных, из которого следует извлечь значение. А название настоящего столбца в базе данных - "IT Resource<u>**s**</u>.Key", поэтому коннектор никогда не мог извлечь из таблицы правильное значение ключа (оно получалось нулевым) и, следовательно, не работал :(
Вот так небольшая опечатка в коде приводит к полной неработоспособности целого модуля и является причиной головной боли у системных администраторов.

Написал в Oracle о проблеме и попросил другую версию коннектора.

P.S. На всякий случай приведу здесь сообщение  об ошибки для индексации поисковиками, вдруг кому-то поможет:
<pre style="background-image: URL(http://2.bp.blogspot.com/_z5ltvMQPaa8/SjJXr_U2YBI/AAAAAAAAAAM/46OqEP32CJ8/s320/codebg.gif); background: #f0f0f0; border: 1px dashed #CCCCCC; color: black; font-family: arial; font-size: 12px; height: auto; line-height: 20px; overflow: auto; padding: 0px; text-align: left; width: 99%;"><code style="color: black; word-wrap: normal;">"The error indicated some resource key is invalid  with  statement
  "com.thortech.xl.exception.ConnectorException: ITResource Key cant be less than or equal to zero"
</code></pre>
If you see the stack trace like the one above while trying to perform Active Directory Reconciliation with Oracle Identity Manager, then you should use another AD Connector version, the version you are using have hard-coded bug in it.
