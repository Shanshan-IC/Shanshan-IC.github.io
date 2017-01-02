---
layout:     post
title:      Leetcode  (73, 74) Matrix Series
category:   [Leetcode] 
tags:		[Leetcode]
---

* [Leetcode 73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

{% highlight C++ %}
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
{% endhighlight %}

* [Leetcode 74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.


For example, Consider the following matrix:

	[
	  [1,   3,  5,  7],
	  [10, 11, 16, 20],
	  [23, 30, 34, 50]
	]

Given target = 3, return true.

{% highlight C++ %}
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
{% endhighlight %}