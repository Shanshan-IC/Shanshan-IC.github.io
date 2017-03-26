---
layout:     post
title:      "Leetcode  (162, 167, 38, 42) Math Series II"
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

## Leetcode 38. Count and Say

* [Leetcode 38. Count and Say](https://leetcode.com/problems/count-and-say/#/description)

The count-and-say sequence is the sequence of integers beginning as follows:
1, 11, 21, 1211, 111221, ...

1 is read off as "one 1" or 11.

11 is read off as "two 1s" or 21.

21 is read off as "one 2, then one 1" or 1211.

Given an integer n, generate the nth sequence.

Note: The sequence of integers will be represented as a string.

```cpp
class Solution {
public:
    string countAndSay(int n) {
        string s = "1";
        for (int i=0; i<n-1; i++)
            s = getNext(s);
        return s;
    }
    
    string getNext(string s) {
        const int n = s.size();
        int count = 1;
        char temp = s[0];
        string res = "";
        for (int i=1; i<n; i++) {
            if (s[i]==s[i-1])   count++;
            else {
                res = res + char(count+int('0')) +temp;
                temp = s[i];
                count = 1;
            }
        }
        res = res + char(count+int('0')) +temp;
        return res;
    }
};
```

## Leetcode 42. Trapping Rain Water

* [Leetcode 42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/#/description)

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example, 
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.

![](/images/water.png)

The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being 

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int res = 0, l = 0, r = height.size()-1;
        while (l < r) {
            int minh = min(height[l], height[r]);
            if (minh == height[l])
                while (++l<r && height[l]<minh)
                    res += minh-height[l];
            else
                while (l<--r && height[r]<minh)
                    res += minh-height[r];
        }
        return res;
    }
};
```