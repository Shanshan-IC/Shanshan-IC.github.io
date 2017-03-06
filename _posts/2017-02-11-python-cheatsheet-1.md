---
layout: post
title:  "Python Cheatsheet: Basic" 
categories: Python
tags:  Python
---

* content
{:toc}

## Name Rule

```python
# for class
MyClass
# for function, module, package, variables
var_separate
# for public
var
# for private
__var
# for internal use
_var
# for protect
_var_
# convention to avoid conflict keyword
var_
# "magic" method or attributes
__var__
```

## __future__
```python
# backport python3 print_function in python2
from __future__ import print_function
print "hello world" # errors

# backport python3 unicode_literals in python2
from __future__ import unicode_literals
print type("Guido")

# Changing the Division Operator
from __future__ import division
print 1/2	#float
print 1//2 #int
```

## Define function __doc__
```python 
def Example():
	""" This is an example function """
	print "example func"

print Example.__doc__
# or
help(Example)
```

## Check, Get, Set attribute, inheritance in Class
```python
class Example(object):
	def __init__(self):
		self.name = "ex"
   	def printex(self):
     	print "This is an example"
ex = Example()
print hasattr(ex, "name")
print getattr(ex,'name')
setattr(ex, name','example')
print issubclass(Example, object)
```

## Check global variables
```python
print globals()
```

## Get Function / Class name
```python
print ex.__class__.__name__
```

## Diamond Problem
```python
# The problem of multiple inheritance in searching a method
def foo_a(self):
	print("This is ClsA")
def foo_b(self):
	print("This is ClsB")
def foo_c(self):
	print("This is ClsC")	

class Type(type):
	def __repr__(cls):
		return cls.__name__

ClsA = Type("ClsA", (object,), {'foo': foo_a})
ClsB = Type("ClsB", (ClsA,), {'foo': foo_b})
ClsC = Type("ClsC", (ClsA,), {'foo': foo_c})
ClsD = Type("ClsD", (ClsB, ClsC), {})
ClsD.mro()
ClsD().foo()				
```

## Smart List
```python
a = [1, 2, 3, 4, 5]
print a[0]
print a[:-1]
print a[0:-1:2]
# copy
ex = [0] * 10
# extend
ex = [1, 2, 3] + ['a', 'b']
# get index and item in the loop
for idx, item in enumerate(a):
	print (idx, item),
```

# Transfer two list into tuple list
```python
zip(a, a)
# with filter
[x for x in a if x>1]
# get distinct val
list(set(a))
# reverse a list
b = a[::-1]
```

## Smart Dictionary
```python
a = {"1":1, "2":2, "3":3}
b = {"2":2, "3":3, "4":4}
print a.keys()
print a.itemes()
# find same key between two dictionary
[_ for _ in a.keys() if _ in b.keys()
# another way
c = set(a).intersection(set(b))
# update dictionary
a.update(b)
```

## for else
```python
for _ in range(5):
	print _,
else:
	print "\n no breaks"
```

## try else
```python
try:
	print "No exception"
except:
	pass
else:
	print "No exception occurred"
```

## lambda function
```python
fn = lambda x: x**2
```

## Option arguments
```python
def example(a, b=None, *args, **kwargs):
	print a, b
	print args
	print kwargs
example(1, "var", 2, 3, word="hello")
```



