---
layout:     post
title:      "Leetcode (45, 55) Jump Game I,II"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

## Leetcode 55. Jump Game

* [Leetcode 55. Jump Game](https://leetcode.com/problems/jump-game/#/description)

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:

A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int temp = 1;
        for (int n:nums) {
            if (temp==0)    return false;
            temp = max(temp-1, n);
        }
        return true;
    }
};
```

## Leetcode 45. Jump Game II

* [Leetcode 45. Jump Game II](https://leetcode.com/problems/jump-game-ii/#/description)

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = [2,3,1,1,4]

The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int res = 0, last = 0, curr = 0;
        for (int i=0; i<nums.size(); i++) {
            if (i>last) {
                last = curr;
                ++res;
            }
            curr = max(curr, i+nums[i]);
        }
        return res;
    }
};
```