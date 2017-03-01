---
layout:     post
title:      Selection Sort and Implementation in Python
category:   [Algorithms] 
tags:       [Algorithms]
---

The algorithm divides the input list into two parts: the sublist of items already sorted, which is built up from left to right at the front (left) of the list, and the sublist of items remaining to be sorted that occupy the rest of the list. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list.

Complexity:

![](/images/algorithms/selection.png)

Example

    64 25 12 22 11 // this is the initial, starting state of the array
    11 25 12 22 64 // sorted sublist = {11}
    11 12 25 22 64 // sorted sublist = {11, 12}
    11 12 22 25 64 // sorted sublist = {11, 12, 22}
    11 12 22 25 64 // sorted sublist = {11, 12, 22, 25}
    11 12 22 25 64 // sorted sublist = {11, 12, 22, 25, 64}

Implementation in Python

{% highlight Python %}
# -*- coding:utf-8 -*-

# 顾名思意,就是直接从待排序数组里选择一个最小(或最大)的数字,每次都拿一个最小数字出来,
# 顺序放入新数组,直到全部拿完

def selection_sort(l):
    for i in range(0, len(l)):
        min_index = i
        min_num =  l[i]
        for j in range(i+1, len(l)):
            if (l[j] < min_num):
                min_index = j
                min_num = l[j]
        l[min_index] = l[i]
        l[i] = min_num
    return l

def main():
    l = [2, 3, 4, 1, 7, 3, 8, 1100, 282828, 1, 20, 0]
    li = selection_sort(l)
    print li

main()
{% endhighlight %}