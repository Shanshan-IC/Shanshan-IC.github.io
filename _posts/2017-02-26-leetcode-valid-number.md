---
layout:     post
title:      "Leetcode (65) Valid Number"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

## Leetcode 65. Valid Number
* [Leetcode 65. Valid Number](https://leetcode.com/problems/valid-number/#/description)

Validate if a given string is numeric.

Some examples:

>	"0" => true
>
>	" 0.1 " => true
>
>	"abc" => false
>
>	"1 a" => false
>
>	"2e10" => true

Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

```cpp
class Solution {
public:
    bool isNumber(string s) {
        int i = 0, k = 0;
        while (s[i]==' ')   i++;
        if (s[i]=='+' || s[i]=='-') i++;
        while (isdigit(s[i])) {
            i++;
            k++;
        }
        if (s[i]=='.')  i++;
        while (isdigit(s[i])) {
            i++;
            k++;
        }
        if (k==0)   return false;
        if (s[i]=='e') {
            i++, k = 0;  
            if(s[i]=='+' || s[i] == '-') i++;  
            while(isdigit(s[i])) i++, k++;  
            if(k == 0) return false;  
        }
        while(s[i] == ' ') i++;  
        return i == s.size();  
    }
};
```