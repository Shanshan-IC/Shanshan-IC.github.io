---
layout:     post
title:      "Leetcode (82, 83) Remove Duplicates from Sorted List I, II"
category:   Leetcode
tags:		Leetcode ListNode
---
* content
{:toc}

Remove Duplicates from Sorted List

## Leetcode 83. Remove Duplicates from Sorted List

* [Leetcode 83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

Given a sorted linked list, delete all duplicates such that each element appear only once.

> For example,
>
> Given 1->1->2, return 1->2.
>
> Given 1->1->2->3->3, return 1->2->3.

```cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* prev = head;
        while (prev) {
            if (prev->next && prev->val == prev->next->val)
                prev->next = prev->next->next;
            else
                prev = prev->next;
        }
        
        return head;
    }
};
```

## Leetcode 82. Remove Duplicates from Sorted List

* [Leetcode 82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

> For example,
>
> Given 1->2->3->3->4->4->5, return 1->2->5.
>
> Given 1->1->1->2->3, return 2->3.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* prevhead = new ListNode(0);
        ListNode* prev = head;
        ListNode* point = prevhead;
        
        while (prev) {
            if (prev->next && prev->val == prev->next->val)
                while (prev->next && prev->val == prev->next->val)
                    prev = prev->next;
            else {
                point->next = prev;
                point = point ->next;
            }
            prev = prev->next;
        }
        point->next = NULL;
        return prevhead->next;
    }
};
```