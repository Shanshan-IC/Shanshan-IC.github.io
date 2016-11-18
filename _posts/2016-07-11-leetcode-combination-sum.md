---
layout:     post
title:      Leetcode  (39, 40) Combination Sum I, II
category:   [Leetcode] 
tags:		[Leetcode, algorithms, recursion]
---

* [Leetcode 39. Combination Sum](https://leetcode.com/problems/combination-sum/)

Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

Note:
* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set [2, 3, 6, 7] and target 7, A solution set is: 
	[
  		[7],
  		[2, 2, 3]
	]

{% highlight C++ %}
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
{% endhighlight %}

* [Leetcode 40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, A solution set is: 
	[
  		[1, 7],
  		[1, 2, 5],
  		[2, 6],
  		[1, 1, 6]
	]

{% highlight C++ %}
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
{% endhighlight %}