---
layout:     post
title:      "Leetcode (485) Math Series III"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Leetcode Math Series III

## Leetcode 485. Max Consecutive Ones

* [Leetcode 485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/#/description)

Given a binary array, find the maximum number of consecutive 1s in this array.

Example 1:

```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```

Note:

* The input array will only contain 0 and 1.

* The length of input array is a positive integer and will not exceed 10,000

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        if (nums.empty())   return 0;
        int res = 0, begin=0, last =-1;
        for (int i = 0; i<nums.size();i++) {
            if (nums[i]==0) {
                res = max(res, last-begin+1);
                begin = i+1;
                last = i;
            } else {
                last++;
            }
        }
        return max(res, last-begin+1);
    }
};
```