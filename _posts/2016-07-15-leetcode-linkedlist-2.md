---
layout:     post
title:      Leetcode  (2)	ListNode Series
category:   [Leetcode] 
tags:		[Leetcode, algorithms, ListNode]
---

* [Leetcode 2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8

{% highlight C++ %}
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        if (!l1)    return l2;
        if (!l2)    return l1;
        int carry = 0;
        ListNode* p = l1;
        ListNode* q = l2;
        ListNode* res = new ListNode(0);
        ListNode* prev = res;
        while (l1 || l2 || carry) {
            int sum = 0;
            if (l1) {
                sum += l1->val;
                l1 = l1->next;
            }
            if (l2) {
                sum += l2->val;
                l2 = l2->next;
            }
            if (carry) {
                sum += carry;
                carry = 0;
            }
            if (sum>9) {
                sum -= 10;
                carry = 1;
            }
            prev->next = new ListNode(sum);
            prev = prev->next;
        }
        return res->next;
    }
};
{% endhighlight %}