---
layout:     post
title:      "Leetcode (73, 74) Matrix Series"
category:   Leetcode 
tags:		Leetcode
---

* content
{:toc}

## Leetcode 73. Set Matrix Zeroes
* [Leetcode 73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        if (matrix.empty()) return;
        const int m = matrix.size();
        const int n = matrix[0].size();
        int row[m] = {0};
        int col[n] = {0};
        for (int i=0; i<m; i++) 
            for (int j=0; j<n; j++)
                if (matrix[i][j] == 0) {
                    row[i] = 1;
                    col[j] = 1;
                }
        for (int i=0; i<m; i++)
            if (row[i] == 1) 
                for (int j=0; j<n; j++)
                    matrix[i][j] = 0;
        for (int j=0; j<n; j++)
            if (col[j] == 1)
                for (int i=0; i<m; i++)
                    matrix[i][j] = 0;
    }
};
```

## Leetcode 74. Search a 2D Matrix

* [Leetcode 74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.


For example, Consider the following matrix:
```
	[
	  [1,   3,  5,  7],
	  [10, 11, 16, 20],
	  [23, 30, 34, 50]
	]
```
Given target = 3, return true.

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty()) return false;
        const int m = matrix.size();
        const int n = matrix[0].size();
        int col = n-1, row = 0;
        while(col>=0 && row<m) {
            if (matrix[row][col] == target) return true;
            else if (matrix[row][col] > target) col--;
            else    row++;
        }
        return false;
    }
};
```

## Leetcode 48. Rotate Image

* [Leetcode 48. Rotate Image](https://leetcode.com/problems/rotate-image/)

You are given an n x n 2D matrix representing an image.

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