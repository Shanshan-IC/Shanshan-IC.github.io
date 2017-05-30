---
layout:     post
title:      "Leetcode (43, 49, 67, 539) String Series II"
category:   Leetcode
tags:		Leetcode Math
---

* content
{:toc}

Leetcode String Series II

## Leetcode 43. Multiply Strings

* [Leetcode 43. Multiply Strings](https://leetcode.com/problems/valid-sudoku/#/description)

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.

Note:

1. The length of both num1 and num2 is < 110.

2. Both num1 and num2 contains only digits 0-9.

3. Both num1 and num2 does not contain any leading zero.

4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

```cpp
class Solution {
public:
    string multiply(string num1, string num2) {
        const int m = num1.size();
        const int n = num2.size();
        string res(m+n+1, '0');
        for (int i=m-1; i>=0; i--)
            for (int j=n-1; j>=0; j--) {
                int temp = (num1[i]-'0')*(num2[j]-'0') + (res[i+j+2]-'0');
                res[i+j+2] = '0'+temp%10;
                res[i+j+1] += temp/10;
            }
        size_t begin = res.find_first_not_of('0');
        if(begin == string::npos) return "0";
        return res.substr(begin);        
    }
};
```

## Leetcode 49. Group Anagrams

* [Leetcode 49. Group Anagrams](https://leetcode.com/problems/anagrams/#/description)

Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 

Return:

`
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
`

Note: All inputs will be in lower-case.

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        if (strs.empty())   return res;
        unordered_map<string, vector<string>> table;
        for (string str: strs) {
            string key = str;
            sort(key.begin(), key.end());
            table[key].push_back(str);
        }
        for (auto i=table.begin(); i!=table.end(); i++) 
            res.push_back(i->second);
        return res;
    }
};
```

## Leetcode 67. Add Binary

* [Leetcode 67. Add Binary](https://leetcode.com/problems/add-binary/#/description)

Given two binary strings, return their sum (also a binary string).

For example,

a = "11"

b = "1"

Return "100".

```cpp
class Solution {
public:
    string addBinary(string a, string b) {
        if (a.empty())  return b;
        if (b.empty())  return a;
        reverse(a.begin(), a.end());
        reverse(b.begin(), b.end());
        int i = 0, j = 0, carry = 0;
        string res = "";
        while (i<a.size() || j<b.size()) {
            if (i<a.size())
                carry += a[i++]-'0';
            if (j<b.size())
                carry += b[j++]-'0';
            res += (char)(carry%2+'0');
            carry /= 2;
        }
        if (carry)  res += '1';
        reverse(res.begin(), res.end());
        return res;
    }
};
```

## Leetcode 539. Minimum Time Difference

* [Leetcode 539. Minimum Time Difference](https://leetcode.com/problems/add-binary/#/description)

Given a list of 24-hour clock time points in "Hour:Minutes" format, find the minimum minutes difference between any two time points in the list.

Example 1:

```
Input: ["23:59","00:00"]
Output: 1
```

Note:

* The number of time points in the given list is at least 2 and won't exceed 20000.

* The input time is legal and ranges from 00:00 to 23:59.

```cpp
class Solution {
public:
    int findMinDifference(vector<string>& timePoints) {
        if (timePoints.empty()) return 0;
        sort(timePoints.begin(), timePoints.end());
        int res = INT_MAX;
        const int n = timePoints.size();
        int val[n] = {0};
        int val2[n] = {0};
        for (int i = 0; i<timePoints.size(); i++) {
            val[i] = stoi(timePoints[i].substr(0,2));
            val2[i] = stoi(timePoints[i].substr(3,2));
        }
        for (int i = 1; i<timePoints.size(); i++) {
            res = min(res, (val[i]-val[i-1])*60+val2[i]-val2[i-1]);
            res = min(res, (val[i-1]+24-val[i])*60+val2[i-1]-val2[i]);
        }
        res = min(res, (val[0]+24-val[n-1])*60+val2[0]-val2[n-1]);
        return res;
    }
};
```