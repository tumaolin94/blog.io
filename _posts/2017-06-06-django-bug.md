---
layout: post
title: solving unittest bug of csrf_token in Django
date: 2017-06-06
categories: blog
tags: [Web Development, python]
description: 

---

in the Chapter 5 of Book "Test-Driven Web Development with Python" written by Harry J.W. Percival, there is a bug in the part of unit test.

while high version of Django(>1.7) rendering template, it will replace the template tag with a `<input type="hidden">`, the value is csrf_token.

```
from django.test import TestCase  
from django.core.urlresolvers import resolve  
from django.http import HttpRequest  
from django.template.loader import render_to_string  
  
from .views import home_page  
  
  
class HomePageTest(TestCase):  
  
    def test_root_url_resolves_to_home_page_view(self):  
        found = resolve('/')  
        self.assertEqual(found.func, home_page)  
  
    def test_home_page_returns_correct_html(self):  
        request = HttpRequest()  
        response = home_page(request)  
        expected_html = render_to_string('home.html')  
        self.assertEqual(response.content.decode(), expected_html)  
```

So with the test code in the book, while running unittest, the respond taken by view function`home_page()` includes `<input>`element, but `render_to_string()` does not build up this part, contributing the fail of test.

the error message is following:

```
$ python3 manage.py test lists  
  
Creating test database for alias 'default'...  
  
F.  
  
======================================================================  
  
FAIL: test_home_page_returns_correct_html (lists.tests.HomePageTest)  
  
----------------------------------------------------------------------  
  
Traceback (most recent call last):  
  
  File "/home/panzeyan/PycharmProjects/TDD/superlists/lists/tests.py", line 20, in test_home_page_returns_correct_html  
  
    self.assertEqual(response.content.decode(), expected_html)  
  
AssertionError: '<htm[240 chars]     <input type=\'hidden\' name=\'csrfmiddlew[184 chars]l>\n' != '<htm[240 chars]     \n        </form>\n\n        <table id="i[87 chars]l>\n'  
  
  
  
----------------------------------------------------------------------  
  
Ran 2 tests in 0.256s  
  
  
  
FAILED (failures=1)  
  
Destroying test database for alias 'default'...  
```

Blog: [http://www.cnblogs.com/panzeyan/p/5819373.html](http://www.cnblogs.com/panzeyan/p/5819373.html), offers a solution, that adding `request=request` while calling `render_to_string` but only Django version from 1.8.x to 1.9.x can solve it.

As a result, my version of Django is 1.10.x, because the token value from view is different from what in the return value of `render_to_string()`.

Until now, I cannot solve the problem with normal way, and even the writter of the book suggests that we should use version 1.8.7, for it is a long term support version.
[https://groups.google.com/forum/#!topic/obey-the-testing-goat-book/fwY7ifEWKMU](https://groups.google.com/forum/#!topic/obey-the-testing-goat-book/fwY7ifEWKMU)

But, I do not want to downdate my version of Dfango, so I devide to use an informal method, using Regular Expression to delete the tag while testing.It is not a suggested method, but you can use it in some special condition.

The code is following:
```
<span style="font-size:10px;">        csrf_regex = r'<input[^>]+csrfmiddlewaretoken[^>]+>'  
        print('expected_html\n',expected_html)  
        observed_html = re.sub(csrf_regex, '', response.content.decode())  
        expected_html = re.sub(csrf_regex, '', expected_html)</span>  
```

