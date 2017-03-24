---
layout:     post
title:      "Leetcode (131, 132) Palindrome Partitioning"
category:   Leetcode
tags:		Leetcode 
---

* content
{:toc}

Leetcode Palindrome Partitioning

## Leetcode 131. Palindrome Partitioning

[Leetcode 131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/#/description)

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return

`
[
  ["aa","b"],
  ["a","a","b"]
]
`

```cpp
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<string> curr;
        vector<vector<string>> res;
        helper(curr, res, s, 0);
        return res;
    }
    
    void helper(vector<string> &curr, vector<vector<string>> &res, string s, int pos) {
        if (pos == s.size())    res.push_back(curr);
        for (int i=pos; i<s.size(); i++) {
            if (isPalindrome(s, pos, i)) {
                curr.push_back(s.substr(pos, i-pos+1));
                helper(curr, res, s, i+1);
                curr.pop_back();
            }
        }
    }
    
    bool isPalindrome(string s, int i, int j){
        while (i<j && s[i]==s[j]){
            i++;
            j--;
        }
        return i>=j;
    }
};
```

## Leetcode 132. Palindrome Partitioning II

[Leetcode 131. Palindrome Partitioning II](https://leetcode.com/problems/palindrome-partitioning-ii/#/description)

Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

For example, given s = "aab",
Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.

```cpp
class Solution {
public:
    int minCut(string s) {
        const int n = s.size();
        vector<vector<int>> isPal(n, vector<int>(n, 0));
        int cut[n] = {0};
        for (int j=0; j<n; j++){
            cut[j] = j;
            for (int i=0; i<=j; i++) {
                if (s[i] == s[j] &&(j-i<=1 || isPal[i+1][j-1])) {
                    isPal[i][j] = 1;
                    if (i>0)    cut[j] = min(cut[j], cut[i-1]+1);
                    else    cut[j] = 0;
                }
            }
        }
        return cut[n-1];
    }
};
```