---
layout:     post
title:      "Leetcode (136, 137, 260) Single Number I, II, III"
category:   Leetcode 
tags:		Leetcode Algorithms Bit
---

* content
{:toc}

Single Number

## Leetcode 136. Single Number

* [Leetcode 136. Single Number](https://leetcode.com/problems/single-number/)

Given an array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for (int n:nums)
            res ^= n;
        return res;
    }
};
```

## Leetcode 137. Single Number II

* [Leetcode 137. Single Number II](https://leetcode.com/problems/single-number-ii/)

Given an array of integers, every element appears three times except for one. Find that single one.

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int one = 0, two = 0;
        for (int n: nums) {
            two |= (n&one);
            one ^= n;
            int t = one & two;
            one &= (~t);
            two &= (~t);
        }
        return one;
    }
};
```

## Leetcode 260. Single Number III

* [Leetcode 260. Single Number III](https://leetcode.com/problems/single-number-iii/)

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example: Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int diff = 0;
        for (int n: nums)   diff^=n;
        diff &= -diff;
        int num1= 0, num2 = 0;
        for (int n:nums) {
            if ((diff & n)==0)    num1 ^= n;
            else num2^=n;
        }
        return {num1, num2};
    }
};
```