---
layout: post
title: Linked List Theory
category: Algorithms
tag: [linkedList, algorithms]
---

Linked List Basic Knowledge (some from geeksforgeeks)

* Concept

Like arrays, Linked List is a linear data structure. Unlike arrays, linked list elements are not stored at contiguous location; the elements are linked using pointers.

{% highlight C++%}
struct node {
	int val;
	node* left;
	node* right;
};
{% endhighlight %}
* Why Linked List?

Arrays can be used to store linear data of similar types, but arrays have following limitations.

1) The size of the arrays is fixed: So we must know the upper limit on the number of elements in advance. Also, generally, the allocated memory is equal to the upper limit irrespective of the usage.

2) Inserting a new element in an array of elements is expensive, because room has to be created for the new elements and to create room existing elements have to shifted.

For example, in a system if we maintain a sorted list of IDs in an array id[].

id[] = [1000, 1010, 1050, 2000, 2040].

And if we want to insert a new ID 1005, then to maintain the sorted order, we have to move all the elements after 1000 (excluding 1000).

Deletion is also expensive with arrays until unless some special techniques are used. For example, to delete 1010 in id[], everything after 1010 has to be moved.

* Advantages over arrays

Dynamic size and Ease of insertion/deletion

* Drawbacks

1) Random access is not allowed. We have to access elements sequentially starting from the first node. So we cannot do binary search with linked lists.

2) Extra memory space for a pointer is required with each element of the list.

Delete an element from a linked list

{% highlight C++ %}
void delNode(ListNode *prev) {
  	ListNode *curr = prev->next;
  	prev->next = curr->next;    
  	delete curr;    // 清理trash指针
}
{% endhighlight %}

* 快慢指针

快慢指的是指针向前移动的步长，一般来说，快指针每次移动 2，慢指针每次移动 1, 主要有两个应用

快速找出未知长度单链表的中间节点
	
	设置两个指针 *fast 和 *slow 都指向头节点
	*fast 移动速度是 *slow 的两倍
	*fast 指向末尾节点时，*slow 正好就在中间

判断单链表是否有环

	设置两个指针 *fast 和 *slow 都指向头节点
	*fast 移动速度是 *slow 的两倍
	如果 *fast == null 说明该单链表不是循环链表
	如果 *fast == *slow 说明该链表是循环链表

其他应用

	找倒数第 N 个节点
	设置两个指针 *fast 和 *slow 都指向头节点
	*fast 先移动 N 步，然后两个指针一起前进
	*fast 到达末尾时，*slow 即为倒数第 N 个节点

* Doubly linked list

Link − Each link of a linked list can store a data called an element.

Next − Each link of a linked list contains a link to the next link called Next.

Prev − Each link of a linked list contains a link to the previous link called Prev.

LinkedList − A Linked List contains the connection link to the first link called First and to the last link called Last.
