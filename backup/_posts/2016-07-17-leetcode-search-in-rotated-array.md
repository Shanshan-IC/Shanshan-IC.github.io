---
layout:     post
title:      Leetcode  (33, 81) Search in Rotated Sorted Array I, II
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Array]
---

* [Leetcode 33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.
{% highlight C++ %}
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if (nums.empty())   return -1;
        int left=0, right = nums.size();
        while (left < right) {
            int mid = left+(right-left)/2;
            if (nums[mid]==target)  return mid;
            if (nums[mid] > nums[left]) {
                if (nums[left]<=target && target<nums[mid])
                    right = mid;
                else
                    left = mid+1;
            }
            else {
                if (nums[mid]<target && target<=nums[right-1])
                    left = mid+1;
                else
                    right = mid;
            }
        }
        return -1;
    }
};
{% endhighlight %}

* [Leetcode 81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.
{% highlight C++ %}
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        if (nums.empty())   return false;
        int left=0, right = nums.size();
        while (left < right) {
            int mid = left+(right-left)/2;
            if (nums[mid]==target)  return true;
            if (nums[mid] > nums[left]) {
                if (nums[left]<=target && target<nums[mid])
                    right = mid;
                else
                    left = mid+1;
            }
            else if (nums[mid] < nums[left]) {
                if (nums[mid]<target && target<=nums[right-1])
                    left = mid+1;
                else
                    right = mid;
            }
            else 
                left++;
        }
        return false;
    }
};
{% endhighlight %}