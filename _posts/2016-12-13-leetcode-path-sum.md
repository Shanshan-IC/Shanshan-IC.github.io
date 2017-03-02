---
layout:     post
title:      "Leetcode (112, 113) Path Sum I, II"
category:   Leetcode 
tags:		Leetcode
---
* content
{:toc}

## Leetcode 112. Path Sum

* [Leetcode 112. Path Sum](https://leetcode.com/problems/path-sum/)

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

```cpp
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if (!root)  return false;
        if (!root->left && !root->right && root->val == sum)    return true;
        return hasPathSum(root->left, sum-root->val) || hasPathSum(root->right, sum-root->val);
    }
};
```

## Leetcode 113. Path Sum II
* [Leetcode 113. Path Sum ii](https://leetcode.com/problems/path-sum-ii/)

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

```
For example: Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

return

	[[5,4,11,2],[5,8,4,5]]
```

```cpp
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> res;
        vector<int> curr;
        if (!root)  return res;
        helper(res, curr, root, sum, 0);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int> &curr, TreeNode* root, int sum, int total) {
        if (!root)  return;
        curr.push_back(root->val);
        total += root->val;
        if (!root->left && !root->right) {
            if (total == sum)   res.push_back(curr);
            curr.pop_back();
            return;
        }
        helper(res, curr, root->left, sum, total);
        helper(res, curr, root->right, sum, total);
        curr.pop_back();
    }
};
```