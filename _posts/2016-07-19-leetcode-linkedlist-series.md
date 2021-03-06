---
layout:     post
title:      "Leetcode  (19, 61, 86, 203) Linked List Series"
category:   Leetcode
tags:		Leetcode LinkedList
---

* content
{:toc}

Linked List Series

## Leetcode 19. Remove Nth Node From End of List

* [Leetcode 19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

Given a linked list, remove the nth node from the end of list and return its head.

For example, Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.

Note: Given n will always be valid. Try to do this in one pass.

```cpp
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
```

## Leetcode 61. Rotate List

* [Leetcode 61. Rotate List](https://leetcode.com/problems/rotate-list/)

Given a list, rotate the list to the right by k places, where k is non-negative.

For example: Given 1->2->3->4->5->NULL and k = 2, return 4->5->1->2->3->NULL.

```cpp
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if (!head || !head->next)   return head;
        ListNode* curr = head;
        int len = 0;
        while (curr) {
            curr = curr->next;
            len++;
        }
        k %= len;
        if (k==0)   return head;
        curr = head;
        ListNode* prev = head;
        while (curr->next) {
            curr = curr->next;
            if (k)
                k--;
            else
                prev=prev->next;
        }
        curr->next = head;
        head = prev->next;
        prev->next = NULL;
        return head;
    }
};
```

## Leetcode 86. Partition List

* [Leetcode 86. Partition List](https://leetcode.com/problems/partition-list/)

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x. You should preserve the original relative order of the nodes in each of the two partitions.

For example, Given 1->4->3->2->5->2 and x = 3, return 1->2->2->4->3->5.

```cpp
class Solution {
public:
    ListNode* partition(ListNode* root, int x) {
        if (!root || !root->next)  return root;
        ListNode* l1 = new ListNode(0);
        ListNode* p1 = l1;
        ListNode* l2 = new ListNode(0);
        ListNode* p2 = l2;
        while (root) {
            if (root->val < x) {
                p1->next = root;
                p1 = p1->next;
            }
            else {
                p2->next = root;
                p2 = p2->next;
            }
            root = root->next;
        }
        p2->next = NULL;
        p1->next = l2->next;
        return l1->next;
    }
};
```

## Leetcode 203. Remove Linked List Elements

* [Leetcode 203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)

Remove all elements from a linked list of integers that have value val.

Example

    Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
    Return: 1 --> 2 --> 3 --> 4 --> 5

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if (!head)  return head;
        head->next = removeElements(head->next, val);
        return head->val==val?head->next:head;
    }
};
```