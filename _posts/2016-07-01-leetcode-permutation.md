{% endhighlight %}{% endhighlight %}e---
layout:     post
title:      Leetcode: Permutation (31, 46, 47, 60)
keywords:   Leetcode
category:   Leetcode 
description: Leetcode
tags:		[Leetcode, algorithms]
---
Leetcode Permutation Serials

Leetcode 31: Next Permutation

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

1,2,3 → 1,3,2

3,2,1 → 1,2,3

1,1,5 → 1,5,1

{% highlight java %}
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
{% endhighlight %}


