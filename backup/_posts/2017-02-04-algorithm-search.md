---
layout:     post
title:      Search Algorithm
category:   [Algorithms] 
tags:       [Algorithms]
---

An algorithm is a step-by-step procedure or method for solving a problem by a computer in a given number of steps. The steps of an algorithm may include repetition depending upon the problem for which the algorithm is being developed. The algorithm is written in human readable and understandable form. 

* Linear Search

A linear search searches an element or value from an array till the desired element or value is not found and it searches in a sequence order. It compares the element with all the other elements given in the list and if the element is matched it returns the value index else it return -1.

{% highlight Python %}
def linear_search(list, val):
    for index, x in enumerate(list):
        if (val == x):
            return index
    return -1

if __name__ == '__main__':
    print linear_search([1, 2, 3, 5, 6, 7, 101010, 1928394, 10299283, 28282829338474], 1928394)
{% endhighlight %}

* Binary Search

{% highlight Python %}
# -*- coding:utf-8 -*-
"""
假设列表从小到大排列，查询一个数字，使用二分法的思想
"""

def binary_search(list, val):
    left = 0
    right = len(list)-1
    while (left<=right):
        mid = left+(right-left)/2
        if val == list[mid] :
            return mid
        elif val < list[mid]:
            right = mid-1
        else:
            left = mid+1
    return -1
{% endhighlight %}

* Hash Table

Hash Table is a data structure which stores data in an associative manner. In a hash table, data is stored in an array format, where each data value has its own unique index value. Access of data becomes very fast if we know the index of the desired data.

Thus, it becomes a data structure in which insertion and search operations are very fast irrespective of the size of the data. Hash Table uses an array as a storage medium and uses hash technique to generate an index where an element is to be inserted or is to be located from.

* Interpolation Search 

Interpolation search is an improved variant of binary search. This search algorithm works on the probing position of the required value. For this algorithm to work properly, the data collection should be in a sorted form and equally distributed.

In binary search, we use mid = (low + high) / 2, in interpolation search, we use mid = low + (key - a[low] / (a[high] - a[low]) * (high - low)) 

{% highlight Python %}
# -*- coding:utf-8 -*-
"""
比如要在取值范围1 ~ 10000 之间 100 个元素从小到大均匀分布的数组中查找5，
会考虑从数组下标较小的开始查找。
经过以上分析，折半查找这种查找方式，还是有改进空间的，并不一定是折半的！
mid = （low+high）/ 2, 即 mid = low + 1/2 * (high - low);
改进为下面的计算机方案（不知道具体过程）：
mid = low + (key - a[low]) / (a[high] - a[low]) * (high - low)，
也就是将上述的比例参数1/2改进了，根据关键字在整个有序表中所处的位置，让mid值的变化更靠近关键字key，
这样也就间接地减少了比较次数。

"""

def interpolation_search(list, val):
    len_list = len(list)
    left = 0
    right = len_list-1
    while (left <= right):
        pos = left + (val-list[left])/(list[right]-list[left])*(right-left)
        if (list[pos] == val):
            return pos
        elif (list[pos] > val):
            right = pos - 1
        else:
            left = pos + 1
    return -1;
{% endhighlight %}