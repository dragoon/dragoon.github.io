---
layout: post
title: "Oracle Fusion Middleware SSO"
date: 2011-08-01
comments: false
categories:
 - Oracle
---


Алилуйа! Наконец-то настроился Single Sign On через Windows Native Authentication в приложениях Oracle Fusion Middleware.

Теперь любой доменный пользователь, имеющий членство в определённой группе, после логина в систему сразу получает доступ к административным консолям Oracle WebLogic, Oracle Access Manager, Oracle Identity Manager и других продуктов из браузеров Internet Explorer и Mozilla Firefox. Вводить пароль в веб-приложении не требутеся, аутентификация происходит автоматически.

Пара ссылок, которые помогли в итоге разобраться с настройкой:
<a href="http://download.oracle.com/docs/cd/E17904_01/core.1111/e12035/confg_sso_admconsoles_im.htm#CEGDJHBE">Configuring Single Sign-on for Administration Consoles</a>
<a href="http://forums.oracle.com/forums/message.jspa?messageID=4053443#4053443%20">http://forums.oracle.com/forums/message.jspa?messageID=4053443#4053443 </a>


