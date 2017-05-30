---
layout:     post
title:      "Leetcode (48, 64, 542) Matrix Series"
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

## Leetcode 542. 01 Matrix

* [Leetcode 542. 01 Matrix](https://leetcode.com/problems/01-matrix/#/description)

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

Example 1: 

Input:

```
0 0 0
0 1 0
0 0 0
```

Output:

```
0 0 0
0 1 0
0 0 0
```

Example 2: 

Input:

```
0 0 0
0 1 0
1 1 1
```

Output:

```
0 0 0
0 1 0
1 2 1
```

Note:

* The number of elements of the given matrix will not exceed 10,000.

* There are at least one 0 in the given matrix.

* The cells are adjacent in only four directions: up, down, left and right.

```cpp
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
        const int n = matrix.size();
        const int m = matrix[0].size();
        typedef pair<int, int> p;
        queue<p> q;
        vector<vector<int>> ans(n, vector<int>(m, 0));
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) 
                if (matrix[i][j] == 1) 
                    ans[i][j] = -1;
                else
                    q.push(p(i, j));
            }
        
        p direct[4] = {p(-1, 0), p(1,0),p(0,1), p(0, -1)};
        while (q.size() > 0) {
            p temp = q.front();
            for (int i = 0; i < 4; i++) {
                int x = temp.first+direct[i].first;
                int y = temp.second+direct[i].second;
                if (x>=0 && x<n && y>=0 && y<m) 
                    if (ans[x][y] == -1) {
                        ans[x][y] = ans[temp.first][temp.second]+1;
                        q.push(p(x, y));
                    }
            }
            q.pop();
        }
        return ans;
        
    }
};
```