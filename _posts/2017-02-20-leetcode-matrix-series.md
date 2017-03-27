---
layout:     post
title:      "Leetcode (48, 64) Matrix Series"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Leetcode Matrix Series

## Leetcode 48. Rotate Image

* [Leetcode 48. Rotate Image](https://leetcode.com/problems/rotate-image/#/description)

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        if (matrix.empty())     return;
        const int n = matrix.size();
        for (int i=0; i<n; i++)
            for (int j=0; j<i; j++)
                swap(matrix[i][j], matrix[j][i]);
        for (int j=0; j<n/2; j++)
            for (int i=0; i<n; i++)
                swap(matrix[i][j], matrix[i][n-1-j]);
    }
};
```

## Leetcode 64. Minimum Path Sum

* [Leetcode 64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/#/description)

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        for (int i=0; i<grid.size(); i++)
            for (int j=0; j<grid[0].size(); j++) {
                if (i==0 && j==0)   continue;
                else    grid[i][j] = min((i-1>=0 ?grid[i-1][j]:INT_MAX), (j-1>=0?grid[i][j-1]:INT_MAX))+grid[i][j];
            }
        return grid.back().back();
    }
};
```