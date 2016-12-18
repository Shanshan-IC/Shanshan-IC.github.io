---
layout:     post
title:      Leetcode  (24, 25)	Swap Nodes
category:   [Leetcode] 
tags:		[Leetcode, Linked List, Recursion]
---

* [Leetcode 24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

Given a linked list, swap every two adjacent nodes and return its head.

For example,

Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

{% highlight C++ %}
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next)  return head;
        ListNode* temp = head->next;
        head->next = swapPairs(head->next->next);
        temp->next = head;
        return temp;
    }
};
{% endhighlight %}


