---
layout:     post
title:      Python Tutorial
category:   [Python] 
tags:       [Python]
---

Python Tutorial

Python is a very simple language, and has a very straightforward syntax. Python uses indentation for blocks, instead of curly braces. Both tabs and spaces are supported, but the standard indentation requires standard Python code to use four spaces.

* Basic Syntax
{% highlight Python %}
# multiple lines, use \ 
total = item_one + \
		item_two 
# if the sentence includes {}, (), [], don't need the \		
days = ['Monday', 'Tuesday', 'Wednesday',
        'Thursday', 'Friday']
{% endhighlight %}
* Python Quotation, '', "", """ (means multiple lines words)
{% highlight Python %}
word = 'word'
sentence = "This is a sentence."
paragraph = """This is a paragraph.
With multiple lines"""
{% endhighlight %}
* Comments
{% highlight Python %}
# this is a comment
'''
There are multiple comments 
here
'''
"""
Multiple comments
"""
{% endhighlight %}
* Python Variables. You do not need to declare variables before using them, or declare their type. 
{% highlight Python %}
# numbers
var1 = 10
myfloat = 1.0
# string, using "" is easy to include '
mystring = 'hello'
mystring = "hello"
mystring = "Don't worry about apostrophes"
mystring = mystring + " " + mystring
# muitlple assignments
a, b = 3, 4
# we will go to details about each variable
{% endhighlight %}
* Operator
{% highlight Python %}
# Arithmetic Operator
a = 21
b = 10
c = a + b
c = a - b
c = a * b
c = a / b
c = a % b
c = a ** b   # power(a, b)
c = a // b   # get the int part

# Comparation Operator
# <  >  ==  !=  >=  <=

# Assignment Operator
# =  +=  -=  *=  /=  %=  **=  //=
# Bit operator
a = 0011 1100
b = 0000 1101
-----------------
a&b = 0000 1100
a|b = 0011 1101
a^b = 0011 0001
~a  = 1100 0011

# Logic Operator
# and or not 

# Member Operator
a = 1
list = [1, 2, 3, 4, 5]
if ( a in list)
	print "a is in the list"

# Identity Operator
a = 20
b = 20
if ( a is b )
	print "a and b have the same identity."
{% endhighlight %}

* Input and Output
{% highlight Python %}
print 'hello, world'
print '100+200 = ', 100+200
{% endhighlight %}



{% highlight Python %}

{% endhighlight %}