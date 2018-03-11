---
layout: post
title: "Language learning flashcards from hearthstone"
date: 2018-03-11
comments: true
categories:
 - hearthstone
 - anki
 - flashcards
---

#### TL;DR
I've generated flashcards for learning words in foreign languages from the names of cards in Hearthstone:
Grab them here: <https://github.com/dragoon/hearthstone-cards>.
----

I really enjoy [Hearthstone](https://playhearthstone.com/) card game from Blizzard.
I also enjoy learning languages.
The Hearthstone dev team @Blizzard is doing tremendous work by translating all their cards, voices and descriptions from English into many other languages.
So I thought about making flash cards based on the card names from the game.
Flash cards facilitate learning new words from foreign languages and they work based on the concept of [spaced repetition](https://en.wikipedia.org/wiki/Spaced_repetition).
The general idea is to repeat what you've learned in regular intervals.
Here is an article about what spaced repetition is and how it works: <https://qz.com/1211561/how-to-learn-a-language-use-spaced-repetition/>

Some Hearthstone enthusiasts have created an API with meta-information about all the cards from Hearthstone, including their names and descriptions:
https://api.hearthstonejson.com/

I've created a script that connects to this API and generates TSV files with card names that can be imported by your favorite program for spaced repetition.
In my case I'm using [Anki](https://apps.ankiweb.net).
For starters I've generated French and German pairs from English and Russian: en-fr, en-de, en-ru and ru-fr, ru-de:
<https://github.com/dragoon/hearthstone-cards>.

Enjoy!

