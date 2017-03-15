---
layout: post
title:  "Python Cheatsheet: Decorator" 
categories: Python
tags:  Python
---

* content
{:toc}

## Why Decorator

Assume we has a function called myfunc, we wanna to call the function in another function. So

![](/images/python/decorator.jpg)

In this way, every time you have to use "deco(myfunc)".

That's why we use the decorator.

![](/images/python/decorator2.jpg)

"@deco" means "myfunc = deco(myfunc)"

# Decorator with parameter

![](/images/python/decorator3.jpg)

"addFunc(3, 8) = deco(True)( addFunc(3, 8))", "myFunc() = deco(False)( myFunc ())"

## Inner Decorator

In python, there are three inner decorator: staticmethod, classmethod, property.

* staticmethod: the difference with method in class is without self. And it can be used without the object.

* classmethod:  the difference with method in class is the first parameter is clf, instead of self.

* property: to get the values in class.

![](/images/python/decorator4.jpg)
