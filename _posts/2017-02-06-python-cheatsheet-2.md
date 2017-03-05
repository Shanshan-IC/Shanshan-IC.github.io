---
layout: post
title:  "Python Cheatsheet: Uniocde" 
categories: Python
tags:  Python
---

* content
{:toc}

## unicode code point to byte
```python
s = u'Café'
print type(s.encode('utf-8'))
```

## byte to unicode code point
```python
s = bytes('Café', encoding = 'utf-8')
print s.decode('tuf-8')
```

## Get unicode code point
```python
for _c in s:print ('U+%04x' % ord(_c))
# python2 str is equivalent to byte string
# python3 str is equivalent to unicode string
```



