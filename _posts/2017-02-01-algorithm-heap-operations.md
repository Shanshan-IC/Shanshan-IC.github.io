---
layout:     post
title:      Heap Operations in Python
category:   [Algorithms] 
tags:       [Algorithms]
---

In python, heapq module offers some operations related to heap.

{% highlight Python %}
# -*- coding:utf-8 -*-

# 使用python自带的包进行heap的相关操作

from heapq import *
from random import shuffle

# 定义堆,建堆
x=[1,2,3,4,5,6]
x = shuffle(x)
heap = []
for i in x:
    heappush(heap, i)
print heap

# 增加要素
heappush(heap, 8)
print heap

# 删除要素
print heappop(heap)
print heap

# 生成堆
x=[1,4,2,3,5,4]
heapify(x)
print x
{% endhighlight %}