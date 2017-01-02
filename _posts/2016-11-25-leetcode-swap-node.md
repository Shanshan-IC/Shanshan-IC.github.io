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

* [Leetcode 25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

For example,

Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5

{% highlight C++ %}
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (!head || k==1)  return head;
        int cnt = 0;
        ListNode* curr = head;
        while (curr && cnt != k) {
            curr = curr ->next;
            cnt++;
        }
        if (cnt == k) {
            curr = reverseKGroup(curr, k);
            while (cnt-- >0){
                ListNode* temp = head->next;
                head->next = curr;
                curr = head;
                head = temp;
            }
            head = curr;
        }
        return head;
    }
};
{% endhighlight %}
