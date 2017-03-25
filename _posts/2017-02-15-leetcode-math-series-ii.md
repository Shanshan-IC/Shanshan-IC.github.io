---
layout:     post
title:      "Leetcode  (162, 167) Math Series II"
category:   Leetcode
tags:		Leetcode Math
---

* content
{:toc}

Math Series II

## Leetcode 162. Find Peak Element

* [Leetcode 162. Find Peak Element](https://leetcode.com/problems/find-peak-element/#/description)

A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        if (nums[0]> nums[1] || nums.size() == 1)
            return 0;
        if ( nums[nums.size()-1] > nums[nums.size()-2])
            return nums.size()-1;
        for (int i=0; i<nums.size()-1; i++) 
            if (nums[i]>nums[i-1] && nums[i]>nums[i+1])
                return i;
        return -1;
    }
};
```

## Leetcode 169. Majority Element

* [Leetcode 169. Majority Element](https://leetcode.com/problems/majority-element/#/description)

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[nums.size()/2];
    }
};
```