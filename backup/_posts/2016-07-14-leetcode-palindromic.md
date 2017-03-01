---
layout:     post
title:      Leetcode  (5, 125)	Palindromic Series
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Palindromic]
---

* [Leetcode 5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example:

	Input: "babad"
	Output: "bab"

	Input: "cbbd"
	Output: "bb"
{% highlight C++ %}
class Solution {
public:
    string longestPalindrome(string s) {
        const int n = s.size();
        if (n<2)    return s;
        int i = 1;
        int res = 0, begin = 0;
        for (int i=0; i<n; i++) {
            int j = i;
            while (j<n && s[j]==s[j+1]) j++;
            int left = i, right = j;
            while (left>=0 && right<n && s[left] == s[right]) {
                left--;
                right++;
            }
            if (right-left-1 > res) {
                res = right - left -1;
                begin = left+1;
            }
        }
        return s.substr(begin, res);
    }
};
{% endhighlight %}

* [Leetcode 125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,

    "A man, a plan, a canal: Panama" is a palindrome.
    "race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

{% highlight C++ %}
class Solution {
public:
    bool isPalindrome(string s) {
        if (s.empty())  return true;
        int left=0, right = s.size()-1;
        while (left<right) {
            while (left<right && !isalnum(s[left]))   left++;
            while (left<right && !isalnum(s[right]))  right--;
            if (left>=right)    break;
            if (tolower(s[left]) != tolower(s[right]))  return false;
            else {
                left++;
                right--;
            }
        }
        return true;
    }
};
{% endhighlight %}



