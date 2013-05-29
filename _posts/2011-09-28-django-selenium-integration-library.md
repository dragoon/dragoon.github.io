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
It's not a secret that testing is an important part of any <b>software development</b>, and if you're building web apps, you definitely need to test your web interface. And it can be a <b>pain in the ass</b> because you need to simulate the process of user interaction with your web app. Luckily, we have such tool as <a href="http://seleniumhq.org/">Selenium</a>.

So in this post I would like to talk about a tool that we have created recently while working on the <a href="http://sciencewise.info/">ScienceWISE</a> project. We have used <b>Selenium</b> in our project since its version 1 branch, and we had a terrible mixture of our code with the code for <b>Selenium</b> integration. So we decided to refactor it and make a separate library. Thus, <a href="https://github.com/dragoon/django-selenium">django-selenium</a> was born. In the rest of this article I will describe the features of this library and how to use it.

<span style="font-size: large;">Features</span>
<ul><li><b>Integration with django test system</b>. <i>django-selenium</i> provides customized test runner built on top of standard django test runner: <b>django_selenium.selenium_runner.SeleniumTestRunner.</b>
You can use it directly in the django settings or subclass to add some custom code.
Behind scenes, <i>SeleniumTestRunner</i> performs the following operations: <ul><li>Runs <b>selenium-server.jar</b></li><li>Runs <b>django test server</b> with appropriate fixtures loaded<b>
</b></li></ul></li><li><b>Writing selenium</b> tests are made simple. Now you can write selenium tests as simple as other django tests: <ul><li>create file <i>seltests.py </i>inside you app</li><li>Subclass your test class from <b>django_selenium.testcases.SeleniumTestCase</b></li><li>Write tests using selenium webriver API!<b>
</b></li></ul>Essentially, <b>SeleniumTestCase </b>just loads required fixtures in a transaction and starts Firefox (or other) driver for you.</li><li><b>Standard webdriver class was extended</b>. We have also written a standard webriver extension called <b>django_selenium.testcases.MyDriver </b>to facilitate common test operations. These operations include: <ul><li><b>authorize() - </b>perform authentication using standard django login url and form</li><li><b>open_url(relative_path) - </b>open some url on a testserver, accepts relative url from <b>reverse() function</b></li><li><b>click(selector) - </b>click on the element found by css selector <b>selector</b> argument</li><li><b>click_and_wait</b>(<b>selector, new_selector</b>) - find and click on the css selector <b>selector</b>, then wait until css selector <b>new_selector </b>is visible</li><li><b>is_element_present(selector)</b> - returns <b>True </b>if element is found by css selector <b>selector</b>, <b>False </b>otherwise.</li></ul>For other functions available, please check the source code. </li></ul>
<span style="font-size: large;">Installation and configuration</span>
Very simple:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">pip install django-selenium
</pre>
Next, specify test runner in your <i>settings.py</i> file:
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">TEST_RUNNER = 'django_selenium.selenium_runner.SeleniumTestRunner'
</pre>
Finally, write a test command that will replace standard django command (you need to place this code in <b>yourapp/management/commands/test.py</b> file):
<pre style="background-color: #eeeeee; border: 1px dashed; margin: 0; padding: 5px;">from django_selenium.management.commands import test_selenium

class Command(test_selenium.Command):

    def handle(self, *test_labels, **options):
        super(Command, self).handle(*test_labels, **options)
</pre>New test command have two additional options:
<ul><li><b>--selenium - </b>run all tests including selenium tests</li><li><b>--selenium-only - <i> </i></b>run only selenium tests</li></ul>As usual, you can run particular selenium test or selenium tests for a particular app.

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
