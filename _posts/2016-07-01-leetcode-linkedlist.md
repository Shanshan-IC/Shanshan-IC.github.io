---
layout:     post
title:      Leetcode  (141, 142) Linked List Cycle I and II
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, LinkedList]
---

[Leetcode 141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

Given a linked list, determine if it has a cycle in it.

Follow up: Can you solve it without using extra space?

The idea: use a fast and a slow pointer, if they are in the same position at some point, that means there exits a cycle inside.
{% highlight C++ %}
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (!head)  return false;
        ListNode* slow = head;
        ListNode* fast = head->next;
        while (fast && fast->next && slow!= fast) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return fast==slow;
    }
};
{% endhighlight %}

[Leetcode 142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
{% highlight C++ %}
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (head==NULL)  return NULL;
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast)
                break;
        }
        if (fast==NULL || fast->next==NULL)
            return NULL;
        slow = head;
        while (slow != fast) {
            slow = slow->next;
            fast = fast->next;
        }
        return fast;
    }
};
{% endhighlight %}