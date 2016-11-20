---
layout: post
title: Stack and Heap Theory
category: Algorithms
tag: [Stack, Heap, algorithms]
---

Stack and Heap Basic Knowledge (some from geeksforgeeks)

* Applications of Heaps:

1) Heap Sort: Heap Sort uses Binary Heap to sort an array in O(nLogn) time.

2) Priority Queue: Priority queues can be efficiently implemented using Binary Heap because it supports insert(), delete() and extractmax(), decreaseKey() operations in O(logn) time. Binomoial Heap and Fibonacci Heap are variations of Binary Heap. These variations perform union also efficiently.

3) Graph Algorithms: The priority queues are especially used in Graph Algorithms 

* Why is Binary Heap Preferred over BST for Priority Queue?

A typical Priority Queue requires following operations to be efficient.
	Get Top Priority Element (Get minimum or maximum)
	Insert an element
	Remove top priority element
	Decrease Key

* why is Binary Heap Preferred for Priority Queue?
	Since Binary Heap is implemented using arrays, there is always better locality of reference and operations are more cache friendly.
	Although operations are of same time complexity, constants in Binary Search Tree are higher.
	We can build a Binary Heap in O(n) time. Self Balancing BSTs require O(nLogn) time to construct.
	Binary Heap doesn’t require extra space for pointers.
	Binary Heap is easier to implement.
	There are variations of Binary Heap like Fibonacci Heap that can support insert and decrease-key in Θ(1) time

* Stack is a linear data structure which follows a particular order in which the operations are performed. The order may be LIFO(Last In First Out) or FILO(First In Last Out).

* Mainly the following three basic operations are performed in the stack:
Push: Adds an item in the stack. If the stack is full, then it is said to be an Overflow condition.

Pop: Removes an item from the stack. The items are popped in the reversed order in which they are pushed. If the stack is empty, then it is said to be an Underflow condition.

Peek: Get the topmost item.

* How to understand a stack practically?

There are many real life examples of stack. Consider the simple example of plates stacked over one another in canteen. The plate which is at the top is the first one to be removed, i.e. the plate which has been placed at the bottommost position remains in the stack for the longest period of time. So, it can be simply seen to follow LIFO/FILO order.

Implementation: http://geeksquiz.com/stack-set-1/

There are two ways to implement a stack:
	
	Using array
	Using linked list

* Applications of stack:

Balancing of symbols:

Infix to Postfix/Prefix conversion

Redo-undo features at many places like editors, photoshop.

Forward and backward feature in web browsers

Used in many algorithms like Tower of Hanoi, tree traversals, stock span problem, histogram problem.

Other applications can be Backtracking, Knight tour problem, rat in a maze, N queen problem and sudoku solver
