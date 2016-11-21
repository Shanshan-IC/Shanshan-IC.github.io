---
layout:     post
title:      Leetcode  (27, 35)   Array Series
category:   [Leetcode] 
tags:       [Leetcode, algorithms, ListNode]
---

* [Leetcode 27. Remove Element](https://leetcode.com/problems/remove-element/)

Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:

Given input array nums = [3,2,2,3], val = 3

Your function should return length = 2, with the first two elements of nums being 2.
{% highlight C++ %}
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int index = 0;
        for (int i=0; i<nums.size(); i++)
            if (nums[i]!=val)
                nums[index++] = nums[i];
        return index;
    }
};
{% endhighlight %}


* [Leetcode 35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

    Here are few examples.
    [1,3,5,6], 5 → 2
    [1,3,5,6], 2 → 1
    [1,3,5,6], 7 → 4
    [1,3,5,6], 0 → 0

{% highlight C++ %}
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        if (nums.empty())   return 0;
        int left = 0, right = nums.size()-1;
        while (left<=right) {
            int mid = left+(right-left)/2;
            if (nums[mid]==target)  return mid;
            else if (nums[mid]<target)  left=mid+1;
            else    right=mid-1;
        }
        return left;
    }
};
{% endhighlight %}