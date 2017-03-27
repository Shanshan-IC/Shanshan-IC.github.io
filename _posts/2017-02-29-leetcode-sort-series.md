---
layout:     post
title:      "Leetcode (75) Sort Series"
category:   Leetcode
tags:		Leetcode DFS
---

* content
{:toc}

Leetcode Sort Series

## Leetcode 75. Sort Colors

* [Leetcode 75. Sort Colors](https://leetcode.com/problems/sort-colors/#/description)

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int zero=0, two=nums.size()-1;
        for (int i=0; i<=two;) {
            if (nums[i]==0) swap(nums[i++], nums[zero++]);
            else if (nums[i]==2)    swap(nums[i], nums[two--]);
            else    i++;
        }
    }
};
```