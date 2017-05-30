---
layout:     post
title:      "Leetcode (98, 99, 543) Binary Tree Series II"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Leetcode Binary Tree Series II

## Leetcode 98. Validate Binary Search Tree

* [Leetcode 98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/#/description)

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys less than the node's key.

* The right subtree of a node contains only nodes with keys greater than the node's key.

* Both the left and right subtrees must also be binary search trees.

Example 1:

```
    2
   / \
  1   3
```

Binary tree [2,1,3], return true.

Example 2:

```
    1
   / \
  2   3
```

Binary tree [1,2,3], return false.

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return helper(root, NULL, NULL);
    }
    
    bool helper(TreeNode* root, TreeNode* minN, TreeNode* maxN) {
        if (!root)  return true;
        if (minN && root->val <= minN->val || maxN && root->val >= maxN->val)   return false;
        return helper(root->left, minN, root) && helper(root->right, root, maxN);
    }
};
```

## Leetcode 99. Recover Binary Search Tree

* [Leetcode 99. Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/#/description)

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

Note:

A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* one = NULL;
    TreeNode* two = NULL;
    TreeNode* pre = new TreeNode(INT_MIN);
    
    void recoverTree(TreeNode* root) {
        help(root);
        swap(one->val, two->val);
    }
    
    void help(TreeNode* root) {
        if (!root)  return;
        help(root->left);
        if (!one && pre->val >= root->val)  one = pre;
        if (one && pre->val >= root->val)  two = root;
        pre = root;
        help(root->right);
    }
};
```

## Leetcode 543. Diameter of Binary Tree

* [Leetcode 543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/#/description)

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:

Given a binary tree 

```
          1
         / \
        2   3
       / \     
      4   5    
```

Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

通过递归计算左右子树的深度来计算根节点的diameter（记为temp），通过和类变量 diameter 进行比较，保存较大值。在每一次递归结束后，返回左右子树的深度，将二者相加再加2就是根节点的diameter。

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int res = 0;
    int getHeight(TreeNode* root) {
        if (!root)  return -1;
        int leftHeight = getHeight(root->left);
        int rightHeight = getHeight(root->right);
        int temp = leftHeight+rightHeight+2;
        res = max(res, temp);
        return max(leftHeight, rightHeight)+1;
    }
    int diameterOfBinaryTree(TreeNode* root) {
        getHeight(root);
        return res;
    }
};
```