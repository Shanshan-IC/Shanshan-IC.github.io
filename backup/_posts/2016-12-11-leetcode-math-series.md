---
layout:     post
title:      Leetcode  (69, 88, 34) Math Series
category:   [Leetcode] 
tags:		[Leetcode]
---
* [Leetcode 69. Sqrt](https://leetcode.com/problems/sqrtx/)

Implement int sqrt(int x).

{% highlight C++ %}
class Solution {
public:
    int mySqrt(int x) {
        long m = x;
        while (m*m >x)
            m = (m+x/m)/2;
        return m;
    }
};
{% endhighlight %}

* [Leetcode 88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

{% highlight C++ %}
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
{% endhighlight %}

* [Leetcode 34. Search for a Range](https://leetcode.com/problems/search-for-a-range/)

Given a sorted array of integers, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,

Given [5, 7, 7, 8, 8, 10] and target value 8,

return [3, 4].

{% highlight C++ %}
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
{% endhighlight %}