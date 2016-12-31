---
layout:     post
title:      Leetcode  (73) Matrix Series
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