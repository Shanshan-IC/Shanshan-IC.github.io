---
layout:     post
title:      Leetcode  (62, 58) Unique Paths I, II
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, DP]
---

* [Leetcode 62. Unique Paths](https://leetcode.com/problems/unique-paths/)

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

{% highlight C++ %}
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        dp[1][0] = 1;
        for (int i=1; i<m+1; i++)
            for (int j=1; j<n+1; j++)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
        return dp[m][n];
    }
};
{% endhighlight %}

* [Leetcode 63. Unique Paths II](hhttps://leetcode.com/problems/unique-paths-ii/)

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.

[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
The total number of unique paths is 2.

{% highlight C++ %}
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if (obstacleGrid.empty())   return 0;
        if (obstacleGrid[0][0] == 1)    return 0;
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                if (i==0 && j==0)   obstacleGrid[i][j] = 1;
                else if (obstacleGrid[i][j]==0) {
                    obstacleGrid[i][j] = (i>=1? obstacleGrid[i-1][j]:0) + (j>=1 ? obstacleGrid[i][j-1]:0);
                }
                else
                    obstacleGrid[i][j] = 0;
            }
        }
        return obstacleGrid[m-1][n-1];
    }
};
{% endhighlight %}