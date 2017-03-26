---
layout:     post
title:      "Leetcode (33) Wildcard Matching"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Leetcode Matrix Series

## Leetcode 44. Wildcard Matching

* [Leetcode 44. Wildcard Matching](https://leetcode.com/problems/wildcard-matching/#/description)

Implement wildcard pattern matching with support for '?' and '*'.
`
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
`

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int i = 0, j = 0, asterick = -1;
        int match;
        while (i < s.size()) {
            if (j<p.size() && p[j]=='*') {
                match = i;
                asterick = j++;
            }
            else if (j<p.size() && (s[i]==p[j] || p[j]=='?')) {
                i++;
                j++;
            }
            else if (asterick >= 0) {
                i = ++match;
                j = asterick+1;
            }
            else    return false;
        }
        while (j<p.size() && p[j]=='*') j++;
        return j==p.size();
    }
};
```