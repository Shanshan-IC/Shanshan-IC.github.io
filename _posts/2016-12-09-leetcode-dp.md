---
layout:     post
title:      Leetcode  (3, 70)	Dynamic Programming
category:   [Leetcode] 
tags:		[Leetcode, algorithms, Math]
---

* [Leetcode 3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

{% highlight C++ %}
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        const int n = s.size();
        int table[256] =  {0};
        int start = 0, res = 0;
        for (int i=0; i<n; i++) {
            table[s[i]]++;
            while (table[s[i]]>1) {
                table[s[start++]]--;   
            }
            res = max(res, i-start+1);    
        }
        return res;
    }
};
{% endhighlight %}

* [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

{% highlight C++ %}
class Solution {
public:
    int climbStairs(int n) {
        int a = 1, b = 1;
        while (n--) 
            a = (b += a) - a;
        return a;
    }
};
{% endhighlight %}


{% highlight C++ %}

{% endhighlight %}