---
layout:     post
title:      Leetcode  (21, 23) Merge Sorted Lists
category:   [Leetcode] 
tags:		[Leetcode, algorithms, linkedList]
---

* [Leetcode 21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

The first Solution is recursion.
{% highlight C++ %}
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* p, ListNode* q) {
        if (!p) return  q;
        if (!q) return p;
        if (p->val < q->val) {
            p->next = mergeTwoLists(p->next, q);
            return p;
        }
        else {
            q->next = mergeTwoLists(p, q->next);
            return q;
        }
    }
};
{% endhighlight %}
The second solution is non-recursion
{% highlight C++ %}
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* p, ListNode* q) {
        if (!p) return  q;
        if (!q) return p;
        ListNode* prev = new ListNode(0);
        ListNode* ans = prev;
        while (p || q) {
            if (p && q) {
                if (p->val < q->val) {
                    ans->next = p;
                    p = p->next;
                }
                else {
                    ans->next = q;
                    q = q->next;
                }
            }
            else if (p) {
                ans->next = p;
                p = p->next;
            }
            else {
                ans->next = q;
                q = q->next;
            }
            ans = ans->next;
        }
        return prev->next;
    }
};
{% endhighlight %}

* [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

The idea: the half recursion to mergeTwolists
{% highlight C++ %}
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        const int n = lists.size();
        if (n==0)   return NULL;
        if (n==1)   return lists[0];
        if (n==2)   return mergeTwoLists(lists[0], lists[1]);
        vector<ListNode*> left(lists.begin(), lists.begin()+n/2);
        vector<ListNode*> right(lists.begin()+n/2, lists.end());
        return mergeTwoLists(mergeKLists(left), mergeKLists(right));
    }
};
{% endhighlight %}
