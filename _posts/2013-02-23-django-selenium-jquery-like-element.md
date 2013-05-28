---
layout: post
title: "Django-selenium jquery-like element selector"
date: 2013-02-23
comments: false
categories:
- django-selenium
- django
- selenium
---

You might know about [django-selenium](https://pypi.python.org/pypi/django-selenium/0.9.5),
the tool [we developed](https://github.com/dragoon/django-selenium/blob/master/AUTHORS) for
django to provide the ability to write selenium tests as easy as normal django tests.
Alongside we've also added numerous *helper methods* that incorporated common use
cases of our (and hopefully other people's) selenium test writing experience (full list of
methods is available at: [https://django-selenium.readthedocs.org/en/latest/#mydriver-class](https://django-selenium.readthedocs.org/en/latest/#mydriver-class))

Until recently, there still remained an annoying problem: django-selenium's find method could only
operate on single (first) element of the css selector. That means when you need other
element than the first one, you had to switch to native selenium's
[find_elements_by_css_selector](http://selenium-python.readthedocs.org/en/latest/api.html#selenium.webdriver.remote.webdriver.find_elements_by_css_selector)
method. Luckily, this problem is solved beautifully in jquery, where by default you can
operate on whole list of elements returned by selector, but at the same time single-element
operations are applied to the first element of the list.

So, I decided to implement the same behaviour for django-selenium. In python it can be easily achieved using the
special [__getattribute__](http://docs.python.org/2/reference/datamodel.html#object.__getattribute__) method,
which allows to intercept every attribute access. Here is the first version of code for
SeleniumElement that serves as a proxy to real selenium elements in django-selenium 0.9.5:

{% highlight python %}
class SeleniumElement(object):
    def __init__(self, elements, selector):
        self.elements = elements
        self.selector = selector
    def __getattribute__(self, name):
        """
        Pass ``__getattribute__`` directly to the first array element.
        """
        attr = object.__getattribute__(self, 'elements')[0].__getattribute__(name)
        return attr
    def __getitem__(self, key):
        """
        Return item from the internal sequence, bypassing ``__getattribute__``
        """
        return object.__getattribute__(self, 'elements')[key]
{% endhighlight %}

Shorty, `__getattribute_` method overwrite will proxy every function call/attribute access to
the underlying first element of the element list returned by selector, and `__getitem__`
method overwrite will be called each time the element is accessed by index, thus returning
the underlying element from the elements list.

Example from the tests:
{% highlight python %}
def test_multiple_elements(self):
    test_list = ['one string', 'another string']
    se = SeleniumElement(test_list, 'selector')
    self.assertEquals(se.replace('one', 'two'), 'two string')
    for i, elem in enumerate(se):
        self.assertEquals(elem, test_list[i])
{% endhighlight %}
