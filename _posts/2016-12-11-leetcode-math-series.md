---
layout:     post
title:      Leetcode  (69, 88) Math Series
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