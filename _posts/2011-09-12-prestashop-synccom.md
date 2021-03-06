---
layout: post
title: "Как создавался новый prestashop-sync.com"
date: 2011-09-12
comments: false
categories:
 - design
 - prestashop-sync
 - how it made
---



Прошло уже больше полугода с тех пор как начал функционировать сервис <a href="http://prestashop-sync.com/">prestashop-sync.com</a>. (Несмотря на то, что мы зарегистрировали этот домен только 27го мая, до этого сервис функционировал на домене **Google App Engine**, prestashop-sync.appspot.com)

На  протяжении всего этого времени, мы постепенно, шаг за шагом, старались  делать сервис лучше и избавлялись от разнообразных ошибок, выявляемых  нашими пользователями.

Первоначально сервис не обладал никаким дизайном, разработка велась хаотично, новые элементы интерфейса накапливались а старые и не думали уходить.

Первичный вариант сервиса можно увидеть на скриншоте ниже:

<a href="http://3.bp.blogspot.com/-bPkSSRQZ_p0/Tm5Cu9x0f0I/AAAAAAAADA0/TW-SksCWRtg/s1600/Prestashop+Sync+Service_old.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="562" src="http://3.bp.blogspot.com/-bPkSSRQZ_p0/Tm5Cu9x0f0I/AAAAAAAADA0/TW-SksCWRtg/s640/Prestashop+Sync+Service_old.png" width="640" /></a>
Вроде бы не очень страшно, но недостатки присутствуют. Интерфейс был сделан в серых невзрачных тонах, повсюду прямоугольные  блоки (пусть и со скруглёнными краями) и такие же кнопочки, плюс к этому отдельные элементы были "удачно" позаимствованы с других сайтов, но в данном контексте выглядели не очень хорошо. Всё это постепенно  начало превращаться в кашу, и поэтому было принято разработать дизайн  сервиса с нуля, но сохранить и улучшить при этом оригинальный процесс  (workflow) работы с сервисом.

Мы пригласили дизайнера, описали предназначение сервиса, функционал, показали сайты, внешний вид которых нам нравится, и попросили сделать пару эскизов.
Первый блин, как обычно, вышел комом:

<a href="http://2.bp.blogspot.com/-D2fZ-PnVsXs/Tm4btYTIiYI/AAAAAAAADAg/5hCHSnVWy9Q/s1600/site_template_v1b.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-D2fZ-PnVsXs/Tm4btYTIiYI/AAAAAAAADAg/5hCHSnVWy9Q/s1600/site_template_v1b.png" /></a>

Я забыл сообщить дизайнеру, что хотелось бы видеть сервис в цветах основного сайта платформы **PrestaShop** - <a href="http://prestashop.com/">prestashop.com</a>, да и общее впечатление было неоднозначным, поэтому работа над дизайном продолжилась.

Второй вариант получился, на наш взгляд, гораздо лучше.  На нём и остановились:

<a href="http://2.bp.blogspot.com/-gyZzhKXqiBw/Tm4bTdn8cMI/AAAAAAAADAc/Bgtq-N4jwp8/s1600/site_template_s2_v1b.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-gyZzhKXqiBw/Tm4bTdn8cMI/AAAAAAAADAc/Bgtq-N4jwp8/s1600/site_template_s2_v1b.png" /></a>
Далее мы продолжили работу над деталями, чтобы сделать сервис максимально удобным и понятным для наших пользователей.

Теперь я подробнее  остановлюсь на различных особенностях нового интерфейса и его отличиях  от старого (помимо совершенного иного общего вида):
<ol><li> Цвета в стили официального сайта **PrestaShop. **
Про это я уже написал выше, мы решили избавиться от засилья серых цветов и сделать что-то более яркое, гамма цветов на сайте PrestaShop довольно неплоха, плюс это создаёт впечатление родства нашего сервиса с оригинальной платформой.</li><li>**Блок описания возможностей сервиса** (Service feature block):
<a href="http://2.bp.blogspot.com/-KOyizpEDPU4/Tm41_hN1TDI/AAAAAAAADAk/u-Ri36_DNgA/s1600/Prestashop+Sync+Service_2.png" imageanchor="1" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="194" src="http://2.bp.blogspot.com/-KOyizpEDPU4/Tm41_hN1TDI/AAAAAAAADAk/u-Ri36_DNgA/s640/Prestashop+Sync+Service_2.png" width="640" /></a>
в блоке имеется возможность динамической смены слайдов, а также можно полностью свернуть блок, причём свёрнутое состояние запоминается, и при последующем заходе на сервис его не нужно будет сворачивать снова.</li><li>**Шаги навигации в непосредственной близости к функционалу.**
В каком-то виде помощь по настройке присутствовала и в старой версии сервиса, но её расположение было не очень удачным, плюс в отведённое под неё количество пространства не получалось уместить более-менее вменяемый текст. Поэтому мы разделили этот блок и добавили соответствующие описания к каждому функциональному блоку в новой версии. Мы также снабдили блоки цифрами, чтобы было понятно, в какой последовательности двигаться:
<a href="http://4.bp.blogspot.com/-YGePNPlcrCo/Tm75nKzbRjI/AAAAAAAADBQ/4CH7qEci8Qw/s1600/Prestashop+Sync+Service_2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://4.bp.blogspot.com/-YGePNPlcrCo/Tm75nKzbRjI/AAAAAAAADBQ/4CH7qEci8Qw/s1600/Prestashop+Sync+Service_2.png" /></a></li><li>**Новая кнопка обновления количества товара.**
В прошлой версии сервиса индикатор процесса обновления количества конкретного товара был сделан в виде вращающегося элемента рядом с кнопкой "обновить":

<a href="http://3.bp.blogspot.com/-tgFNk5u7CDE/Tm5J4k-KShI/AAAAAAAADBA/TC4chUVEiaM/s1600/loader1.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-tgFNk5u7CDE/Tm5J4k-KShI/AAAAAAAADBA/TC4chUVEiaM/s1600/loader1.png" /></a><a href="http://4.bp.blogspot.com/-2qGNl5y1TWo/Tm5J5JlxRfI/AAAAAAAADBE/OD8pR7ZZESE/s1600/ok1.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://4.bp.blogspot.com/-2qGNl5y1TWo/Tm5J5JlxRfI/AAAAAAAADBE/OD8pR7ZZESE/s1600/ok1.png" /></a>
В новой версии мы пошли дальше, ведь кнопка не нужна пока процесс обновления не закончится, и мы совместили эти элементы. Получилось удобно и красиво:

<a href="http://3.bp.blogspot.com/-kn8xm9ri9jk/Tm47f-ZM04I/AAAAAAAADAo/HxXCoKv4ePY/s1600/loader2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-kn8xm9ri9jk/Tm47f-ZM04I/AAAAAAAADAo/HxXCoKv4ePY/s1600/loader2.png" /></a><a href="http://1.bp.blogspot.com/-He7ht5ZzPkk/Tm47gMu2kNI/AAAAAAAADAs/VY3tpD5iZmA/s1600/ok2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://1.bp.blogspot.com/-He7ht5ZzPkk/Tm47gMu2kNI/AAAAAAAADAs/VY3tpD5iZmA/s1600/ok2.png" /></a></li><li>У каждого магазина в списке есть индикатор состояния: зелёный - значит всё хорошо и можно работать с магазином, красный - произошла ошибка и работать пока нельзя. Раньше у нас была отдельная кнопка обновления статуса в колонке действия. Но зачем отдельная кнопка для обновления статуса если можно совместить и статус и кнопку?

Таким образом мы добились уменьшения разнообразия индикаторов и действий при одновременном сохранении удобства использования:
<a href="http://3.bp.blogspot.com/-ZKpgyniu6yA/Tm71OqHDKrI/AAAAAAAADBI/Flrea70Oaq0/s1600/status.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-ZKpgyniu6yA/Tm71OqHDKrI/AAAAAAAADBI/Flrea70Oaq0/s1600/status.png" /></a></li><li>**Трапециевидные кнопки.**
Ещё одна наша находка - нестандартные кнопки в форме трапеции. По реализации этот элемент оказался одним из самых сложных, но выглядят они, на наш взгляд, очень эффектно:
<a href="http://4.bp.blogspot.com/-s6qU-msGYeo/Tm8aM3_t6eI/AAAAAAAADBY/kRo0bb8jqgw/s1600/buttons.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://4.bp.blogspot.com/-s6qU-msGYeo/Tm8aM3_t6eI/AAAAAAAADBY/kRo0bb8jqgw/s1600/buttons.png" /></a></li><li>**Показ количества статей.**
Идея довольна проста - пусть наши посетители сразу видят количество имеющихся на нашем сайте статей. Пока число статей не очень большое - это может быть актуально:
<a href="http://3.bp.blogspot.com/-RTZa4bGL1oI/Tm8ZKdHwWeI/AAAAAAAADBU/QBHlpgPFjcM/s1600/Prestashop+Sync+Service_2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://3.bp.blogspot.com/-RTZa4bGL1oI/Tm8ZKdHwWeI/AAAAAAAADBU/QBHlpgPFjcM/s1600/Prestashop+Sync+Service_2.png" /></a></li></ol>
