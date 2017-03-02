---
layout:     post
title:      "Leetcode (96, 97) Unique Binary Search Trees I, II"
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