---
layout:     post
title:      "Leetcode (95, 96) Unique Binary Search Trees I, II"
category:   Leetcode 
tags:		Leetcode
---
* content
{:toc}

## Leetcode 96. Unique Binary Search Trees

* [Leetcode 96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)

Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,

Given n = 3, there are a total of 5 unique BST's.

```cpp
class Solution {
public:
    int numTrees(int n) {
        int res[n+1] = {0};
        res[0] = res[1] = 1;
        for (int i=2; i<=n; i++)
            for (int j=1; j<=i; j++)
                res[i] += res[j-1] * res[i-j];
        return res[n];
    }
};
```

## Leetcode 95. Unique Binary Search Trees II

* [Leetcode 95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

`
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
`

idea: 当数组为 1，2，3，4，.. i，.. n时，基于以下原则的BST建树具有唯一性
以i为根节点的树，其左子树由[1, i-1]构成， 其右子树由[i+1, n]构成。

```cpp
class Solution {
public:
    vector<TreeNode*> help_tree(int first, int last) {
        vector<TreeNode*> res;
        for (int root=first; root<last+1; root++) {
            auto left = root==first ? vector<TreeNode*>{nullptr}:help_tree(first, root-1);
            auto right = root==last ? vector<TreeNode*>{nullptr}:help_tree(root+1, last);
            for (auto l:left)
                for (auto r:right) {
                    TreeNode *node = new TreeNode(root);
                    node -> left = l;
                    node -> right = r;
                    res.push_back(node);
                }
        }
        return res;
    }
    
    vector<TreeNode*> generateTrees(int n) {
        return help_tree(1, n);
    }
};
```