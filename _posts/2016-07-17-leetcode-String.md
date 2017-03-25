---
layout:     post
title:      "Leetcode  (14, 58, 151, 179) String Series"
category:   Leetcode
tags:		Leetcode String
---

* content
{:toc}

String Series

## Leetcode 58. Length of Last Word

* [Leetcode 58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string. If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example,  Given s = "Hello World", return 5.

```cpp
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
```

## Leetcode 14. Longest Common Prefix

* [Leetcode 14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

Write a function to find the longest common prefix string amongst an array of strings.

```cpp
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
```

## Leetcode 151. Reverse Words in a String

* [Leetcode 151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/#/description)

```cpp
class Solution {
public:
    void reverseWords(string &s) {
        istringstream input(s);
        string res, temp;
        while(input>>temp) 
            res = " "+ temp + res;
        s = res.empty()?res: res.substr(1);
    }
};
```

## Leetcode 179. Largest Number

* [Leetcode 179. Largest Number](https://leetcode.com/problems/largest-number/)

Given a list of non negative integers, arrange them such that they form the largest number.

For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.

```cpp
class Solution {
public:
    string largestNumber(vector<int>& nums) {
        const int n = nums.size();
        vector<string> str(n);
        for (int i=0; i<n; i++)
            str[i] = to_string(nums[i]);
        sort(str.begin(), str.end(), [](string &i, string &j){return i+j>j+i;});
        string res;
        for (string s:str)  res+=s;
        return res[0]=='0'?"0":res;
    }
};
```