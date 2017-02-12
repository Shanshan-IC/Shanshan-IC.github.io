---
layout:     post
title:      Odd_Even Sort and Implementation in Python
category:   [Algorithms] 
tags:       [Algorithms]
---

It functions by comparing all odd/even indexed pairs of adjacent elements in the list and, if a pair is in the wrong order (the first is larger than the second) the elements are switched. The next step repeats this for even/odd indexed pairs (of adjacent elements). Then it alternates between odd/even and even/odd steps until the list is sorted.

Example

Given a list [6 2 4 1 5 9]

    a. Odd turn: [2 6 1 4 5 9]
    b. Even turn: [2 1 6 4 5 9]
    c. Odd turn: [1 2 4 6 5 9]
    d. Even turn: [1 2 4 5 6 9]

Complexity

![](/images/algorithms/odd.png)

Pseudocode

{% highlight Python %}
algorithm quicksort(A, lo, hi) is
    if lo < hi then
        p := partition(A, lo, hi)
        quicksort(A, lo, p – 1)
        quicksort(A, p + 1, hi)

algorithm partition(A, lo, hi) is
    pivot := A[hi]
    i := lo     // place for swapping
    for j := lo to hi – 1 do
        if A[j] ≤ pivot then
            swap A[i] with A[j]
            i := i + 1
    swap A[i] with A[hi]
    return i
{% endhighlight %}

Implementation in Python

{% highlight Python %}
# -*- coding:utf-8 -*-

# 又一个比较性质的排序,基本思路是奇数列排一趟序,偶数列排一趟序,再奇数排,再偶数排,直到全部有序

def odd_even_sort(l):
    flag = True
    flag = True
    for i in range(len(l) - 1):
        if flag:
            flag = False
            for j in range(1, len(l), 2):
                if l[j] > l[j + 1]:
                    flag = True
                    l[j], l[j + 1] = l[j + 1], l[j]
            for j in range(0, len(l) - 1, 2):
                if l[j] > l[j + 1]:
                    flag = True
                    l[j], l[j + 1] = l[j + 1], l[j]

def main():
    l = [2, 3, 4, 1, 7, 3, 8, 1100, 282828, 1, 20, 0]
    li = odd_even_sort(l)
    print li

main()

{% endhighlight %}