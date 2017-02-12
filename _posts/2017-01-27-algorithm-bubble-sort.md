---
layout:     post
title:      Bubble Sort and Implementation in Python
category:   [Algorithms] 
tags:       [Algorithms]
---


Bubble sort, sometimes referred to as sinking sort, is a simple sorting algorithm that repeatedly steps through the list to be sorted, compares each pair of adjacent items and swaps them if they are in the wrong order. 

Complexity:

![](/images/algorithms/bubble.png)

Example

First Pass

	( 5 1 4 2 8 ) {\displaystyle \to } \to  ( 1 5 4 2 8 ), Here, algorithm compares the first two elements, and swaps since 5 > 1.
	( 1 5 4 2 8 ) {\displaystyle \to } \to  ( 1 4 5 2 8 ), Swap since 5 > 4
	( 1 4 5 2 8 ) {\displaystyle \to } \to  ( 1 4 2 5 8 ), Swap since 5 > 2
	( 1 4 2 5 8 ) {\displaystyle \to } \to  ( 1 4 2 5 8 ), Now, since these elements are already in order (8 > 5), algorithm does not swap them.

Second Pass

	( 1 4 2 5 8 ) {\displaystyle \to } \to  ( 1 4 2 5 8 )
	( 1 4 2 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 ), Swap since 4 > 2
	( 1 2 4 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 )
	( 1 2 4 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 )

Now, the array is already sorted, but the algorithm does not know if it is completed. The algorithm needs one whole pass without any swap to know it is sorted.

Third Pass

	( 1 2 4 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 )
	( 1 2 4 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 )
	( 1 2 4 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 )
	( 1 2 4 5 8 ) {\displaystyle \to } \to  ( 1 2 4 5 8 )

Pseudocode

{% highlight Python %}
procedure bubbleSort( A : list of sortable items )
   n = length(A)
   repeat 
     swapped = false
     for i = 1 to n-1 inclusive do
       /* if this pair is out of order */
       if A[i-1] > A[i] then
         /* swap them and remember something changed */
         swap( A[i-1], A[i] )
         swapped = true
       end if
     end for
   until not swapped
end procedure
{% endhighlight %}

Implementation in Python

{% highlight Python %}
# -*- coding:utf-8 -*-
# 原理是临近的数字两两进行比较,按照从小到大或者从大到小的顺序进行交换,
# 这样一趟过去后,最大或最小的数字被交换到了最后一位,
# 然后再从头开始进行两两比较交换,直到倒数第二位时结束

def bubble_sort(l):
    len_l = len(l)
    for i in range(0, len_l-1):
        for j in range(i, len_l):
            if (l[i] > l[j]):
                l[i], l[j] = l[j], l[i]
    return l

def main():
    l = [2, 3, 4, 1, 7, 3, 8, 1100, 282828, 1, 20, 0]
    li = bubble_sort(l)
    print li

main()

{% endhighlight %}