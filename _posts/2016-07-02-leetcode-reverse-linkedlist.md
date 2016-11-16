---
layout:     post
title:      Leetcode  (206, 92) Reverse Linked List I and II
category:   [Leetcode] 
tags:		[Leetcode, algorithms, linkedList]
---

[Leetcode 206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

Reverse a singly linked list.

{% highlight C++ %}
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next)
            return head;
        ListNode* newHead = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return newHead;
    }
};
{% endhighlight %}

[92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:

Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.
{% highlight C++ %}
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        ListNode* prehead = new ListNode(0);
        prehead->next = head;
        ListNode* tail = prehead;
        n -= m;
        while(--m > 0) tail = tail->next;
        ListNode* curr = tail->next;
        while(n-- > 0){ // pull one out to tail
            ListNode* temp = curr->next;
            curr->next = temp->next; 
            temp->next = tail->next; // easy to make mistake
            tail->next = temp;
        }
        return prehead->next;
    }
};
{% endhighlight %}