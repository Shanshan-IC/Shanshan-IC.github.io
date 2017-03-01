---
layout:     post
title:      "Leetcode (1, 15, 16, 18) Sum Series"
category:   Leetcode
tags:		Leetcode Algorithms Math
---
* content
{:toc}

Leetcode Sum Serials

## Leetcode 1. Two Sum

* [Leetcode 1. Two Sum](https://leetcode.com/problems/two-sum/)

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

	Example:
	Given nums = [2, 7, 11, 15], target = 9,
	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].

The idea: use the map to store the value's index, and for loop the map to find m[target-nums[i]] exits in the map

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        const int n = nums.size();
        unordered_map<int, int> m;
        for (int i=0; i<n; i++)
            m[nums[i]] = i;
        for (int i=0; i<n; i++) {
            if (m[target-nums[i]]) {
                res.push_back(i);
                res.push_back(m[target-nums[i]]);
                break;
            }
        }
        return res;
    }
};
```

## Leetcode 15. 3Sum

* [Leetcode 15. 3Sum](https://leetcode.com/problems/3sum/)

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

	For example, given array S = [-1, 0, 1, 2, -1, -4],
	A solution set is:
	[
  		[-1, 0, 1],
  		[-1, -1, 2]
	]

The idea: sort the nums, and then start at i, j=i+1, and k is the last number, if the sum is smaller, then j++, if it is bigger, then k--;

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        const int n = nums.size();
        if (n<3)    return res;
        sort(nums.begin(), nums.end());
        for (int i=0; i<n; i++) {
            int j = i+1, k = n-1;
            while (j<k) {
                while (j<k && nums[i]+nums[j]+nums[k] < 0) j++;
                while (j<k && nums[i]+nums[j]+nums[k] > 0) k--;
                if (j<k && nums[i]+nums[j]+nums[k] == 0) {
                    res.push_back({nums[i], nums[j], nums[k]});
                    while (j<k && nums[j]==nums[j+1])   j++;
                    j++;
                    while (j<k && nums[k]==nums[k-1])   k--;
                }
            }
            while (i<n && nums[i]==nums[i+1])   i++;
        }
        return res;
    }
};
```

## LeetCode 16. 3Sum Closest

* [LeetCode 16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.
    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

The idea: sort the nums, keep trace the newest closet answer and difference.

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int ans = nums[0]+nums[1]+nums[2];
        int diff = abs(target - ans);
        if (diff==0)    return ans;
        const int n = nums.size();
        sort(nums.begin(), nums.end());
        for (int i=0; i<n; i++) {
            int j = i+1;
            int k = n-1;
            while (j<k) {
                int temp = nums[i]+nums[j]+nums[k];
                int newDiff = abs(target-temp);
                if (newDiff<diff) {
                    ans = temp;
                    diff = newDiff;
                }
                if (temp<target)    j++;
                else    k--;
            }
        }
        return ans;
    }
};
```

## LeetCode 18. 4Sum

* [LeetCode 18. 4Sum](https://leetcode.com/problems/4sum/)

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note: The solution set must not contain duplicate quadruplets.
	For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.
	A solution set is:
	[
  		[-1,  0, 0, 1],
  		[-2, -1, 1, 2],
  		[-2,  0, 0, 2]
	]

The idea is same as the 3Sum.

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        const int n = nums.size();
        if (n<4)    return res;
        sort(nums.begin(), nums.end());
        for (int i=0; i<n; i++) {
            for (int j=i+1; j<n; j++) {
                int k = j+1;
                int m = n-1;
                while (k<m) {
                while (k<m && nums[i]+nums[j]+nums[k]+nums[m] < target) k++;
                while (k<m && nums[i]+nums[j]+nums[k]+nums[m] > target) m--;
                if (k<m && nums[i]+nums[j]+nums[k]+nums[m] == target) {
                    res.push_back({nums[i], nums[j], nums[k], nums[m]});
                    while (k<m && nums[k]==nums[k+1])   k++;
                    k++;
                    while (k<m && nums[m]==nums[m-1])   m--;
                }
                }
                while (j<n && nums[j]==nums[j+1])   j++;
            }
            while (i<n && nums[i]==nums[i+1])   i++;
        }
        return res;
    }
};
```