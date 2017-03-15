---
layout: post
title:  "Python Cheatsheet: Exception" 
categories: Python
tags:  Python
---

* content
{:toc}

## Try except

```python
try:
    open("abc.txt",'r')
except IOError:
    print "Cannot open the file!" 
```

```python
try:
    print  aa
except  NameError, msg:
    print  msg
```

## Try finally
Whatever to catch up the errors, still run the finally
```python 
import time

try:
    f = file('poem.txt')
    while True: # our usual file-reading idiom
        line = f.readline()
        if len(line) == 0:
            break
        time.sleep(2)
        print line,
finally:
    f.close()
    print 'Cleaning up...closed the file'
```

## Throw out errors Raise
```python
filename = raw_input('please input file name:')
if filename=='hello':
    raise NameError('input file name error !')
```

## Check all the threads inside
```python
import exceptions
dir(exceptions)
```
