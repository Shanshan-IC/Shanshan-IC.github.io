---
layout:     post
title:      Leetcode  (19) ListNode Series
category:   [Leetcode] 
tags:		[Leetcode, algorithms, ListNode]
---

* [Leetcode 20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.
   After removing the second node from the end, the linked list becomes 1->2->3->5.

Note:
Given n will always be valid.
Try to do this in one pass.
{% highlight C++ %}
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* prev = new ListNode(0);
        prev->next = head;
        ListNode* prehead = prev;
        while (n--) head = head->next;
        ListNode* curr = head;
        while (head) {
            prehead=prehead->next;
            head=head->next;
        }
        prehead->next = prehead->next->next;
        return prev->next;
    }
};
{% endhighlight %}