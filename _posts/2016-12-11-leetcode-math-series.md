---
layout:     post
title:      "Leetcode (69, 88, 34, 507) Math Series II"
category:   Leetcode 
tags:		Leetcode
---

* content
{:toc}

## Leetcode 69. Sqrt

* [Leetcode 69. Sqrt](https://leetcode.com/problems/sqrtx/)

Implement int sqrt(int x).

```cpp
class Solution {
public:
    int mySqrt(int x) {
        long m = x;
        while (m*m >x)
            m = (m+x/m)/2;
        return m;
    }
};
```

## Leetcode 88. Merge Sorted Array
* [Leetcode 88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m-1, j = n-1, k = m + n - 1;
        while (j>=0) {
            if (i>=0 && nums2[j] < nums1[i])
                nums1[k--] = nums1[i--];
            else 
                nums1[k--] = nums2[j--];
        }
    }
};
```

## Leetcode 34. Search for a Range

* [Leetcode 34. Search for a Range](https://leetcode.com/problems/search-for-a-range/)

Given a sorted array of integers, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,

Given [5, 7, 7, 8, 8, 10] and target value 8,

return [3, 4].

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res;
        if (nums.empty())   return res;
        int left = 0, right = nums.size()-1;
        while (left<=right) {
            int mid = left + (right-left)/2;
            if (nums[mid] == target) {
                int i = mid, j = mid;
                while (i-1>=0 && nums[i-1]== nums[i])   i--;
                while (j+1<nums.size() && nums[j+1]== nums[j])   j++;
                return {i, j};
            }
            else if (nums[mid] < target)
                left = mid+1;
            else    right = mid-1;
        }
        return {-1, -1};
    }
};
```

## Leetcode 507. Perfect Number

* [Leetcode 507. Perfect Number](https://leetcode.com/problems/perfect-number/#/description)

We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.

Example:

```
Input: 28
Output: True
Explanation: 28 = 1 + 2 + 4 + 7 + 14
```

Note: The input number n will not exceed 100,000,000. (1e8)

```cpp
class Solution {
public:
    bool checkPerfectNumber(int num) {
        if (num==1) return false;
        int temp = sqrt(num);
        int sum = num-1;
        for (int i = 2; i <= temp; i++) {
            if (num%i==0)  {
                if (i==temp && temp*temp==num)  sum-=i;
                else    sum= sum-i-num/i;
            }
            if (sum<0) return false;
        }
        
        return sum==0;
    }
};
```
