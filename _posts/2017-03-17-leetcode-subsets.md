---
layout:     post
title:      "Leetcode  (78, 90) Subsets I, II"
category:   Leetcode
tags:		Leetcode DFS
---

* content
{:toc}

## Leetcode 78. Subsets

* [Leetcode 78. Subsets](https://leetcode.com/problems/subsets/#/description)

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:

`
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
`

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> curr;
        helper(res, curr, nums, 0);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int> &curr, vector<int> &nums, int pos) {
        res.push_back(curr);
        for (int i=pos; i<nums.size(); i++) {
            curr.push_back(nums[i]);
            helper(res, curr, nums, i+1);
            curr.pop_back();
        }
    }
};
```

## Leetcode 90. Subsets II

* [Leetcode 90. Subsets II](https://leetcode.com/problems/subsets-ii/#/description)

Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,

If nums = [1,2,2], a solution is:

`
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
`

```cpp
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> curr;
        sort(nums.begin(), nums.end());
        helper(res, curr, nums, 0);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int> &curr, vector<int> &nums, int pos) {
        res.push_back(curr);
        for (int i=pos; i<nums.size(); i++) {
            curr.push_back(nums[i]);
            helper(res, curr, nums, i+1);
            while (nums[i]==nums[i+1])  i++;
            curr.pop_back();
        }
    }
};
```