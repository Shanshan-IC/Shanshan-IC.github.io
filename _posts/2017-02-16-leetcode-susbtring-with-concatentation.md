---
layout:     post
title:      "Leetcode 30 Substring with Concatenation of All Words"
category:   Leetcode
tags:       Leetcode Math
---

* content
{:toc}

## Leetcode 30. Substring with Concatenation of All Words

* [Leetcode 30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/#/description)

You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

For example, given:

s: "barfoothefoobarman"

words: ["foo", "bar"]

You should return the indices: [0,9].
(order does not matter).

```cpp
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
        vector<int> res;
        if (s.empty() || words.empty()) return res;
        map<string, int> word;
        map<string, int> curr;
        for (string str: words) word[str]++;
        int m = words[0].size();
        int n = words.size();
        if (s.size()<m*n)   return res;
        for (int i=0; i<=s.size()-m*n; i++) {
            curr.clear();
            int j = 0;
            for (j=0; j<n; j++) {
                string temp = s.substr(i+j*m, m);
                if (word.find(temp)==word.end())    break;
                curr[temp]++;
                if (curr[temp]>word[temp])  break;
            }
            if (j==n)   res.push_back(i);
        }
        return res;
    }
};
```