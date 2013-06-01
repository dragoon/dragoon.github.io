---
layout: post
title: "Django Selenium integration Library"
date: 2011-09-28
comments: false
categories:
 - sciencewise
 - django
 - selenium
---


Original article (in Russian): <a href="http://habrahabr.ru/blogs/django/129107/">http://habrahabr.ru/blogs/django/129107/</a>

Hi there.
It's not a secret that testing is an important part of any **software development**, and if you're building web apps, you definitely need to test your web interface. And it can be a **pain in the ass** because you need to simulate the process of user interaction with your web app. Luckily, we have such tool as <a href="http://seleniumhq.org/">Selenium</a>.

So in this post I would like to talk about a tool that we have created recently while working on the <a href="http://sciencewise.info/">ScienceWISE</a> project. We have used **Selenium** in our project since its version 1 branch, and we had a terrible mixture of our code with the code for **Selenium** integration. So we decided to refactor it and make a separate library. Thus, <a href="https://github.com/dragoon/django-selenium">django-selenium</a> was born. In the rest of this article I will describe the features of this library and how to use it.

<span style="font-size: large;">Features</span>
<ul><li>**Integration with django test system**. *django-selenium* provides customized test runner built on top of standard django test runner: **django_selenium.selenium_runner.SeleniumTestRunner.**
You can use it directly in the django settings or subclass to add some custom code.
Behind scenes, *SeleniumTestRunner* performs the following operations: <ul><li>Runs **selenium-server.jar**</li><li>Runs **django test server** with appropriate fixtures loaded**
**</li></ul></li><li>**Writing selenium** tests are made simple. Now you can write selenium tests as simple as other django tests: <ul><li>create file *seltests.py *inside you app</li><li>Subclass your test class from **django_selenium.testcases.SeleniumTestCase**</li><li>Write tests using selenium webriver API!**
**</li></ul>Essentially, **SeleniumTestCase **just loads required fixtures in a transaction and starts Firefox (or other) driver for you.</li><li>**Standard webdriver class was extended**. We have also written a standard webriver extension called **django_selenium.testcases.MyDriver **to facilitate common test operations. These operations include: <ul><li>**authorize() - **perform authentication using standard django login url and form</li><li>**open_url(relative_path) - **open some url on a testserver, accepts relative url from **reverse() function**</li><li>**click(selector) - **click on the element found by css selector **selector** argument</li><li>**click_and_wait**(**selector, new_selector**) - find and click on the css selector **selector**, then wait until css selector **new_selector **is visible</li><li>**is_element_present(selector)** - returns **True **if element is found by css selector **selector**, **False **otherwise.</li></ul>For other functions available, please check the source code. </li></ul>
<span style="font-size: large;">Installation and configuration</span>
Very simple:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">pip install django-selenium
</pre>
Next, specify test runner in your *settings.py* file:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">TEST_RUNNER = 'django_selenium.selenium_runner.SeleniumTestRunner'
</pre>
Finally, write a test command that will replace standard django command (you need to place this code in **yourapp/management/commands/test.py** file):
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">from django_selenium.management.commands import test_selenium

class Command(test_selenium.Command):

    def handle(self, *test_labels, **options):
        super(Command, self).handle(*test_labels, **options)
</pre>New test command have two additional options:
<ul><li>**--selenium - **run all tests including selenium tests</li><li>**--selenium-only - * ***run only selenium tests</li></ul>As usual, you can run particular selenium test or selenium tests for a particular app.

That's all. Now I have created an example app for you to check all this functionality instantly:
<a href="https://github.com/dragoon/django-selenium-testapp">https://github.com/dragoon/django-selenium-testapp</a>.

Lest try it.
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;"># Download selenium-server.jar
wget http://selenium.googlecode.com/files/selenium-server-standalone-2.7.0.jar

git clone git://github.com/dragoon/django-selenium-testapp.git
cd django-selenium-testapp
# set path to selenium-server.jar in SELENIUM_PATH
vi settings.py

# Run tests
./manage.py test --selenium-only
...
----------------------------------------------------------------------
Ran 1 test in 13.254s

OK
</pre>
If everyting is fine, you should have seen the following on the screen:
<a href="http://habrastorage.org/storage1/645184cd/0b5a1717/7e0296d1/768b2894.png" imageanchor="1" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="342" src="http://habrastorage.org/storage1/645184cd/0b5a1717/7e0296d1/768b2894.png" width="640" /></a>
Please report any issues to <a href="https://github.com/dragoon/django-selenium/issues">https://github.com/dragoon/django-selenium/issues</a>.
