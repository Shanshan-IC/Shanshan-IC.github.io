---
layout:     post
title:      "Leetcode  (39, 40) Combination Sum I, II"
category:   Leetcode
tags:		Leetcode Recursion
---
* content
{:toc}

Combination Sum

## Leetcode 39. Combination Sum

* [Leetcode 39. Combination Sum](https://leetcode.com/problems/combination-sum/)

Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

Note:
* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set [2, 3, 6, 7] and target 7, A solution set is: 
	
```
[
	[7],
	[2, 2, 3]
]
```

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> curr;
        sort(candidates.begin(), candidates.end());
        helper(res, curr, candidates, target, 0);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int>& curr, vector<int>& candidates, int target, int pos) {
        if (target==0) {
            res.push_back(curr);
            return;
        }
        for (int i=pos; i<candidates.size() && target>0; i++) {
            curr.push_back(candidates[i]);
            helper(res, curr, candidates, target-candidates[i], i);
            curr.pop_back();
        }
    }
};
```

## Leetcode 40. Combination Sum II
* [Leetcode 40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, A solution set is: 

```
[
	[1, 7],
	[1, 2, 5],
	[2, 6],
	[1, 1, 6]
]
```

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> curr;
        sort(candidates.begin(), candidates.end());
        helper(res, curr, candidates, target, 0);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int>& curr, vector<int>& candidates, int target, int pos) {
        if (target==0) {
            res.push_back(curr);
            return;
        }
        for (int i=pos; i<candidates.size() && target>0; i++) {
            curr.push_back(candidates[i]);
            helper(res, curr, candidates, target-candidates[i], i+1);
            curr.pop_back();
            while (i<candidates.size() && candidates[i]==candidates[i+1])   i++;
        }
    }
};
```

## Leetcode 77. Combinations

* [Leetcode 77. Combinations](https://leetcode.com/problems/combinations/)

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example, If n = 4 and k = 2, a solution is:

```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> curr;
        if (n<k)    return res;
        helper(res, curr, 1, n, k);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int> &curr, int pos, int n, int k) {
        if (k==0) {
            res.push_back(curr);
            return;
        }
        for (int i=pos; i<=n && k>0; i++) {
            curr.push_back(i);
            helper(res, curr, i+1, n, k-1);
            curr.pop_back();
        }
    }
    
};
```