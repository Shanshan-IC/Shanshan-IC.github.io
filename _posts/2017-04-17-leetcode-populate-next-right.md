---
layout:     post
title:      "Leetcode (116, 117) Populating Next Right Pointers in Each Node I, II"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Populating Next Right Pointers in Each Node

## Leetcode 116. Populating Next Right Pointers in Each Node

* [Leetcode 116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/#/description)

Given a binary tree

```
    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

Note:

* You may only use constant extra space.

* You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

For example,
Given the following perfect binary tree,

```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
```

After calling your function, the tree should look like:

```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
```

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if (!root)  return;
        if (root -> left) {
            root-> left -> next = root -> right;
            if (root -> next)
                root -> right -> next = root -> next -> left;
        }
        connect(root -> left);
        connect(root -> right);
    }
};
```

## Leetcode 117. Populating Next Right Pointers in Each Node II

* [Leetcode 117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/#/description)

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

You may only use constant extra space.
For example,
Given the following binary tree,

```
         1
       /  \
      2    3
     / \    \
    4   5    7
```

After calling your function, the tree should look like:

```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if (!root)  return;
        TreeLinkNode dummy(INT_MIN);
        for (TreeLinkNode *cur = root, *pre = &dummy; cur; cur = cur->next) {
            if (cur -> left) {
                pre -> next = cur -> left;
                pre = pre -> next;
            } 
            if (cur -> right) {
                pre -> next = cur -> right;
                pre = pre -> next;
            }
        }
        connect(dummy.next);
        
    }
};
```