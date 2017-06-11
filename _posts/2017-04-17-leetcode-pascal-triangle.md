---
layout:     post
title:      "Leetcode (118, 119) Pascal's Triangle I, II"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Pascal's Triangle

## Leetcode 118. Pascal's Triangle

* [Leetcode 118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/#/description)

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return

```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> res;
        for (int i = 0; i < numRows; i++) {
            res.push_back(vector<int>(i+1, 1));
            for (int j = 1; j < i; j++)
                res[i][j] = res[i-1][j-1] + res[i-1][j];
        }
        return res;
    }
};
```

## Leetcode 119. Pascal's Triangle II

* [Leetcode 118. Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/#/description)

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> res(rowIndex + 1);
        res[0] = 1;
        for (int i = 0; i <= rowIndex; i++)
            for (int j = i; j > 0; j--)
                res[j] = res[j] + res[j-1];
        return res;
    }
};
```