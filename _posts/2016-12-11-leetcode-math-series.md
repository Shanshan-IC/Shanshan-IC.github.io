---
layout:     post
title:      Leetcode  (69) Math Series
category:   [Leetcode] 
tags:		[Leetcode]
---
* [Leetcode 69. Sqrt](https://leetcode.com/problems/sqrtx/)

Implement int sqrt(int x).

{% highlight C++ %}
class Solution {
public:
    int mySqrt(int x) {
        long m = x;
        while (m*m >x)
            m = (m+x/m)/2;
        return m;
    }
};
{% endhighlight %}


