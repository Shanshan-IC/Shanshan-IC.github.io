---
layout:     post
title:      Leetcode  (14, 58) String Series
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Binary Tree, Recursion]
---

* [Leetcode 58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 
Given s = "Hello World",
return 5.
{% highlight C++ %}
class Solution {
public:
    int lengthOfLastWord(string s) {
        int len = 0;
        if (s.empty())  return 0;
        const int n = s.size();
        for (int i=0; i<n; i++) {
            if (s[i] != ' ')    len++;
            else {
                while (i<n && s[i]==' ')   i++;
                if (i<n && s[i]!=' ')   len = 1;
            }
        }
        return len;
    }
};
{% endhighlight %}

* [Leetcode 14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

Write a function to find the longest common prefix string amongst an array of strings.
{% highlight C++ %}
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string res;
        if (strs.empty())   return res;
        for (int i=0; i<strs[0].size(); i++) {
            char temp = strs[0][i];
            for (int j=1; j<strs.size(); j++) {
                if (i>=strs[j].size() || strs[j][i]!=temp)
                    return res;
            }
            res+=temp;
        }
        return res;
    }
};
{% endhighlight %}