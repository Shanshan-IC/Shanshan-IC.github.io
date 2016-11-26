---
layout:     post
title:      Leetcode  (4, 80)	emove Duplicates from Sorted Array I, II
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Array]
---

* [Leetcode 26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

{% highlight C++ %}
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty())   return 0;
        int index = 0;
        for (int i=1; i<nums.size(); i++) {
            if (nums[i]!=nums[index])
                nums[++index] = nums[i];
        }
        return index+1;
    }
};
{% endhighlight %}

* [Leetcode 80. Remove Duplicates from Sorted Array II]

Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.

{% highlight C++ %}
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int index = 1;
        const int n = nums.size();
        if (n<2)    return n;
        for (int i=1; i<n; i++) {
            if (i+1<n && nums[i-1]==nums[i] && nums[i]==nums[i+1])
                continue;
            nums[index++] = nums[i];
        }
        return index;
    }
};
{% endhighlight %}


{% highlight C++ %}

{% endhighlight %}