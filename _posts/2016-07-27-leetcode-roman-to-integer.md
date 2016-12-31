---
layout:     post
title:      Leetcode  (12, 13) Roman to Integer and reverse
category:   [Leetcode] 
tags:		[Leetcode]
---


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