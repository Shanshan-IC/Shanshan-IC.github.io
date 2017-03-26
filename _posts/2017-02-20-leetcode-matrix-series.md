---
layout:     post
title:      "Leetcode Matrix Series"
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



