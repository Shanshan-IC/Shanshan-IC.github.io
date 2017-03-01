---
layout:     post
title:      "Leetcode (31, 46, 47, 60) Permutation"
category:   Leetcode
tags:		Leetcode Algorithms
---

* content
{:toc}

Leetcode Permutation Serials

## Leetcode 31. Next Permutation

[Leetcode 31. Next Permutation](https://leetcode.com/problems/next-permutation)

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        if (nums.size() < 2)
            return;
        int i, j;
        for (i = nums.size() - 2; i >= 0; i--)
            if (nums[i] < nums[i + 1])
                break;
        for (j = nums.size() - 1; j > i; j--)
            if (nums[i] < nums[j])
                break;
        if (i >= 0)
            swap(nums[i], nums[j]);
        reverse(nums.begin() + i + 1, nums.end());
    }
};
```

## Leetcode 46. Permutations
[Leetcode 46. Permutations](https://leetcode.com/problems/permutations/)

Given a collection of distinct numbers, return all possible permutations.

For example, [1,2,3] have the following permutations:

```
    [
        [1,2,3],
        [1,3,2],
        [2,1,3],
        [2,3,1],
        [3,1,2],
        [3,2,1]
    ]
```

```cpp
class Solution {
public:
    vector<vector<int> > permute(vector<int> &num) {
        vector<vector<int> > result;
        
        helper(result, 0, num);
        return result;
    }
    
    void helper(vector<vector<int>> &res, int begin, vector<int>& nums) {
        if (begin >= nums.size()) {
            res.push_back(nums);
            return;
        }
        for (int i=begin; i<nums.size(); i++) {
            swap(nums[i], nums[begin]);
            helper(res, begin+1, nums);
            swap(nums[i], nums[begin]);
        }
    }
};
```

## Leetcode 47. Permutations II

[Leetcode 47. Permutations II](https://leetcode.com/problems/permutations-ii/)

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example, [1,1,2] have the following unique permutations:

```
    [   
        [1,1,2],
        [1,2,1],
        [2,2,1],
    ]
```

```cpp
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        helper(res, 0, nums);
        return res;
    }
    
    void helper(vector<vector<int>> &res, int begin, vector<int>& nums) {
        if (begin >= nums.size()) {
            res.push_back(nums);
            return;
        }
        for (int i=begin; i<nums.size(); i++) {
            
            swap(nums[i], nums[begin]);
            helper(res, begin+1, nums);
            swap(nums[i], nums[begin]);
            while (i<nums.size() && nums[i]==nums[i-1])
                i++;
        }
    }
};
```

## Leetcode 60. Permutation Sequence

[Leetcode 60. Permutation Sequence](https://leetcode.com/problems/permutation-sequence/)

The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, We get the following sequence (ie, for n = 3):

1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"

Given n and k, return the kth permutation sequence.

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        vector<int> input(n);
        for (int i=1; i<=n; i++)
            input[i-1] = i;
        k--;
        string res;
        while (input.size()>1) {
            int f = fac(input.size()-1);
            int pos = k/f;
            res += input[pos] +'0';
            input.erase(input.begin()+pos);
            k %= f;
        }
        res += input[0] +'0';
        return res;
    }
    
    int fac(int n) {
        if (n==0)   return 1;
        int res = 1;
        for (int i=1; i<=n; i++)
            res *= i;
        return res;
    }
};
```