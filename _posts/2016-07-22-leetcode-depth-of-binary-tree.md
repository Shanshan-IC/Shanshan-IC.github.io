---
layout:     post
title:      "Leetcode  (110, 111) Depth of Binary Tree"
category:   Leetcode 
tags:		Leetcode BinaryTree
---
* content
{:toc}
Binary Tree

## Leetcode 110. Balanced Binary Tree

*[Leetcode 110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        if (!root)  return true;
        int left = depth(root->left);
        int right = depth(root->right);
        return abs(left-right)<=1 && isBalanced(root->left) && isBalanced(root->right);
    }
    
    int depth(TreeNode* root) {
        if (!root)  return 0;
        return 1+max(depth(root->left), depth(root->right));
    }
};
```

## Leetcode 111. Minimum Depth of Binary Tree

* [Leetcode 111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (!root)  return 0;
        if (!root->left && !root->right)    return 1;
        if (!root->left)    return 1+minDepth(root->right);
        if (!root->right)   return 1+minDepth(root->left);
        return 1+min(minDepth(root->left), minDepth(root->right));
    }
};
```