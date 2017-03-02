---
layout:     post
title:      "Leetcode (235, 236) Lowest Common Ancestor"
category:   Leetcode
tags:		Leetcode BinaryTree BST
---

* content
{:toc}

## Leetcode 235. Lowest Common Ancestor of a Binary Search Tree

* [Leetcode 235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of [LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root->val < p->val && root->val < q->val)
            return lowestCommonAncestor(root->right, p, q);
        if (root->val > p->val && root->val > q->val)
            return lowestCommonAncestor(root->left, p, q);
        return root;
    }
};
```

## Leetcode 236. Lowest Common Ancestor of a Binary Tree

* [Leetcode 236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
         if (!root || root==p || root == q) return root;
         TreeNode* t1 = lowestCommonAncestor(root->left, p, q);
         TreeNode* t2 = lowestCommonAncestor(root->right, p, q);
         if (t1 && t2)  return root;
         return t1 ? t1:t2;
    }
};
```