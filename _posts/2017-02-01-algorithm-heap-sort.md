---
layout:     post
title:      "Heap Sort and Implementation in Python"
category:   Algorithms 
tags:       Algorithms
---

* content
{:toc}

## Heap Sort

The heapsort algorithm involves preparing the list by first turning it into a max heap. The algorithm then repeatedly swaps the first value of the list with the last value, decreasing the range of values considered in the heap operation by one, and sifting the new first value into its position in the heap. This repeats until the range of considered values is one value in length.

The steps are:

a. Call the buildMaxHeap() function on the list. Also referred to as heapify(), this builds a heap from a list in O(n) operations.

b. Swap the first element of the list with the final element. Decrease the considered range of the list by one.

c. Call the siftDown() function on the list to sift the new first element to its appropriate index in the heap.

d. Go to step b unless the considered range of the list is one element.

## Example

Given a list [6 2 4 1 5 9]

a. pick the first number 6, and compare other numbers with 6, the bigger one is put in the right, otherwise in the lef, so it become: [2 4 1 5 6 9]

b. then quick sort the left part [2 4 1 5] and the right part [9], continue step a, it will become: [1 2 4 5], so the result is [1 2 4 5 6 9]

## Complexity

![](/images/algorithms/heap.png)

## Pseudocode

```python
procedure heapsort(a, count) is
    input: an unordered array a of length count
 
    (Build the heap in array a so that largest value is at the root)
    heapify(a, count)

    (The following loop maintains the invariants that a[0:end] is a heap and every element
     beyond end is greater than everything before it (so a[end:count] is in sorted order))
    end ← count - 1
    while end > 0 do
        (a[0] is the root and largest value. The swap moves it in front of the sorted elements.)
        swap(a[end], a[0])
        (the heap size is reduced by one)
        end ← end - 1
        (the swap ruined the heap property, so restore it)
        siftDown(a, 0, end)
```

## Implementation in Python

```python
def heapify(l, n, i):
    maxs = i
    left = 2*i+1
    right = 2*i+2
    if (left<n and l[left]>l[maxs]):
        maxs = left
    if (right<n and l[right]>l[maxs]):
        maxs = right
    if (maxs!=i):
        l[i], l[maxs] = l[maxs], l[i]
        heapify(l, n, maxs)

def heap_sort(l):
    size = len(l)
    for i in range(size/2-1, -1, -1):
        heapify(l, size, i)
    for j in range(size-1, -1, -1):
        l[0], l[j] = l[j], l[0]
        heapify(l, j, 0)
    return l

def main():
    l = [2, 3, 4, 1, 7, 3, 8, 1100, 282828, 1, 20, 0]
    li = heap_sort(l)
    print li

main()

```