---
layout:     post
title:      "Insertion Sort and Implementation in Python"
category:   Algorithms 
tags:       Algorithms
---
* content
{:toc}

## Insertion Sort

Insertion sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. In this post, we only present the 

## Complexity

![](/images/algorithms/insert2.png)

## Example

![](/images/algorithms/insert.png)

## Pseudocode

```python
for i ← 1 to length(A)
    j ← i
    while j > 0 and A[j-1] > A[j]
        swap A[j] and A[j-1]
        j ← j - 1
    end while
end for
```

## Implementation in Python

```python
# -*- coding:utf-8 -*-

# 插入排序就是每一步都将一个待排数据按其大小插入到已经排序的数据中的适当位置，直到全部插入完毕。
# 插入排序方法分直接插入排序和折半插入排序两种，这里只介绍直接插入排序

def insert_sort(l):
    for i in range(1,len(l)):
        if (l[i]<l[i-1]):
            temp = l[i]
            j = i
            while (j>0 and l[j-1]>temp):
                l[j] = l[j-1]
                j = j-1
            l[j] = temp
    return l


def main():
    l = [2, 3, 4, 1, 7, 3, 8, 1100, 282828, 1, 20, 0]
    li = insert_sort(l)
    print li

main()
```