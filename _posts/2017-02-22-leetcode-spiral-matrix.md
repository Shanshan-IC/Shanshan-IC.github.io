---
layout:     post
title:      "Leetcode (54) Spiral Matrix I, II"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Leetcode Spiral Matrix

## Leetcode 54. Spiral Matrix

* [Leetcode 54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/#/description)

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

`
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
`

You should return [1,2,3,6,9,8,7,4,5].

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        if (matrix.empty()) return res;
        const int m = matrix.size();
        const int n = matrix[0].size();
        int left = 0, right = n-1, up = 0, down = m-1, dir = 0;
        for (int k=0, i=0, j=0; k<m*n; k++) {
            res.push_back(matrix[i][j]);
            if (dir == 0) {
                if (j==right) {
                    i++;
                    dir = 1;
                    up++;
                }
                else    j++;
            }  else if (dir == 1) {
                if (i==down) {
                    j--;
                    dir = 2;
                    right--;
                } 
                else  i++;
            } else if (dir == 2) {
                if (j==left) {
                    dir = 3;
                    i--;
                    down--;
                }
                else    j--;
            } else {
                if (i==up) {
                    dir = 0;
                    j++;
                    left++;
                }
                else    i--;
            }
        }
        return res;
    }
};
```

## Leetcode 59. Spiral Matrix II

* [Leetcode 59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/#/description)

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:

`
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
`

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> table(n, vector<int>(n, 0));
        int i = 0, j =0, k=1;
        while (k<=n*n) {
            while (j<n && table[i][j]==0)   table[i][j++] = k++;
            i++;j--;
            while (i<n && table[i][j]==0)   table[i++][j] = k++;
            i--;j--;
            while (j>=0 && table[i][j]==0)   table[i][j--] = k++;
            i--;j++;
            while (i>=0 && table[i][j]==0)   table[i--][j] = k++;
            i++;j++;
        }
        return table;
    }
};
```