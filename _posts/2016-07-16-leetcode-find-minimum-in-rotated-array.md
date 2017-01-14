---
layout:     post
title:      Leetcode  (153, 154) Find Minimum in Rotated Sorted Array I, II
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Array]
---

* [Leetcode 153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate exists in the array.
{% highlight C++ %}
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left = 0, right = nums.size()-1;
        while (left < right) {
            int mid = left+(right-left)/2;
            if (nums[left] < nums[right])
                return nums[left];
            else if (nums[left]<nums[mid])
                left = mid;
            else if (nums[left]>nums[mid])
                right = mid;
            else
                left++;
        }
        return nums[left];
    }
};
{% endhighlight %}

* [Leetcode 154. Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

Follow up for "Find Minimum in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

In the same way, it can be used in the duplicated cases.
{% highlight C++ %}
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left = 0, right = nums.size()-1;
        while (left < right) {
            int mid = left+(right-left)/2;
            if (nums[left] < nums[right])
                return nums[left];
            else if (nums[left]<nums[mid])
                left = mid;
            else if (nums[left]>nums[mid])
                right = mid;
            else
                left++;
        }
        return nums[left];
    }
};
{% endhighlight %}