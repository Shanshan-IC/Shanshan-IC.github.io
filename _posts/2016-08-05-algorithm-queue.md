---
layout: post
title: "Queue Theory"
category: Algorithms
tag: Queue Algorithms
---

* content
{:toc}

Queue Basic Knowledge (some from geeksforgeeks)

## Queue

Queue is a linear structure which follows a particular order in which the operations are performed. The order is First In First Out (FIFO). 

The difference between stacks and queues is in removing. In a stack we remove the item the most recently added; in a queue, we remove the item the least recently added.

## Operations on Queue

Mainly the following four basic operations are performed on queue:
Enqueue: Adds an item to the queue. If the queue is full, then it is said to be an Overflow condition.

Dequeue: Removes an item from the queue. The items are popped in the same order in which they are pushed. If the queue is empty, then it is said to be an Underflow condition.

Front: Get the front item from queue.

Rear: Get the last item from queue.

## Applications of Queue:

Queue is used when things don’t have to be processed immediatly, but have to be processed in First InFirst Out order like Breadth First Search. This property of Queue makes it also useful in following kind of scenarios.

1) When a resource is shared among multiple consumers. Examples include CPU scheduling, Disk Scheduling.

2) When data is transferred asynchronously (data not necessarily received at same rate as sent) between two processes. Examples include IO Buffers, pipes, file IO, etc.

## Array implementation Of Queue

For implementing queue, we need to keep track of two indices, front and rear. We enqueue an item at the rear and dequeue an item from front. If we simply increment front and rear indices, then there may be problems, 
front may reach end of the array. The solution to this problem is to increase front and rear in circular manner

## Priority Queue is an extension of queue with following properties.

1) Every item has a priority associated with it.

2) An element with high priority is dequeued before an element with low priority.

3) If two elements have the same priority, they are served according to their order in the queue.

## A typical priority queue supports following operations.

insert(item, priority): O(1)

getHighestPriority(): Returns the highest priority item. O(n)

deleteHighestPriority(): Removes the highest priority item.

We can also use Linked List, time complexity of all operations with linked list remains same as array. The advantage with linked list is deleteHighestPriority() can be more efficient as we don’t have to move items.

## How to implement priority queue?

Using Array: A simple implementation is to use array of following structure.

```cpp
struct item {
   int item;
   int priority;
}
```

## Using Heaps

Heap is generally preferred for priority queue implementation because heaps provide better performance compared arrays or linked list. In a Binary Heap, getHighestPriority() can be implemented in O(1) time, insert() can be implemented in O(Logn) time and deleteHighestPriority() can also be implemented in O(Logn) time.

With Fibonacci heap, insert() and getHighestPriority() can be implemented in O(1) amortized time and deleteHighestPriority() can be implemented in O(Logn) amortized time.

``` Some operations

Check it's full

front==(rear+1)%n

Check it's empty

front == rear
