---
layout:     post
title:      Leetcode  (7)	Math
category:   [Leetcode] 
tags:		[Leetcode, algorithms, math]
---

* [Leetcode 7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

{% highlight C++ %}
class Solution {
public:
    int reverse(int x) {
        bool neg =false;
        long y = x;
        if (y<0)
        {
             y = -y;
             neg = true;
        }
        long res = 0;
        while (y)
        {
            res = res *10+y%10;
            y /= 10;
        }
        if (!neg && res > INT_MAX || neg && -res < INT_MIN)
            return 0;
        return (neg)?-res:res;
    }
}; 
{% endhighlight %}

* [Leetcode 9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

Determine whether an integer is a palindrome. Do this without extra space.

{% highlight C++ %}
class Solution {
public:
    bool isPalindrome(int x) {
        int val = 0;
        int k = x;
        if (x<0)    return false;
        while (k) {
            int temp = k%10;
            val = val*10 + temp;
            k /= 10;
        }
        return val == x;
    }
};
{% endhighlight %}

* [Leetcode 11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

{% highlight C++ %}
class Solution {
public:
    int maxArea(vector<int>& nums) {
        if (nums.empty())   return 0;
        int left = 0, right = nums.size()-1;
        int res = 0;
        while (left<right) {
            int temp = (right-left)*min(nums[left], nums[right]);
            res = max(res, temp);
            if (nums[left]<nums[right]) left++;
            else    right--;
        }
        return res;
    }
};
{% endhighlight %}
