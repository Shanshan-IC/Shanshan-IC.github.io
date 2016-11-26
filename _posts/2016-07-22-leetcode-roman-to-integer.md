---
layout:     post
title:      Leetcode  (12, 13) Roman to Integer and reverse
category:   [Leetcode] 
tags:		[Leetcode, Algorithms]
---

* [Leetcode 12. Integer to Roman](https://leetcode.com/problems/integer-to-roman/)

{% highlight C++ %}
class Solution {
public:
    string intToRoman(int num) {
        vector<string> M = {"", "M", "MM", "MMM"};
        vector<string> C = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        vector<string> X = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        vector<string> I = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[num/1000] + C[num%1000/100] + X[num%100/10] + I[num%10];
    }
};
{% endhighlight %}

* [Leetcode 13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

{% highlight C++ %}
class Solution {
public:
    int romanToInt(string s) {
        int size = s.size();
        if (size == 0)
            return 0;
        unordered_map<char, int> set = {{'I', 1},
                                        {'V', 5},
                                        {'X', 10},
                                        {'L', 50},
                                        {'C', 100},
                                        {'D', 500},
                                        {'M', 1000}
        };
        int sum = set[s.back()];
        for (int i=s.size()-2; i>=0; i--)
        {
            if (set[s[i]] < set[s[i+1]])
                sum -= set[s[i]];
            else 
                sum += set[s[i]];
        }
        return sum;
    }
};
{% endhighlight %}