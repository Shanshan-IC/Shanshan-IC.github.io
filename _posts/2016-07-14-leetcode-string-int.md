---
layout:     post
title:      "Leetcode  (8)	String with Int"
category:   Leetcode
tags:		Leetcode String
---

* content
{:toc}
String 

## Leetcode 8. String to Integer (atoi)
* [Leetcode 8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

```cpp
class Solution {
public:
    int myAtoi(string str) {
        if (str.empty())    return 0;
        long long res = 0;
        bool neg = false;
        
        int i  = 0;
        while (str[i]==' ') i++;
        if (str[i]=='+')  {neg = false;i++;}
        else if(str[i]=='-')    {neg = true;i++;}
        
        for (; i<str.size(); i++) {
            if (str[i]<'0' || str[i]>'9')   break;
            res = res*10 + (str[i]-'0');
            if (neg && -res<INT_MIN)    return INT_MIN;
            if (!neg && res>INT_MAX)    return INT_MAX;
        }
        if (neg)
            return -res<INT_MIN?INT_MIN:-res;
        else
            return res>INT_MAX?INT_MAX:res;
    }
};
```