---
layout:     post
title:      Leetcode  (231, 326, 342) Power of 2, 3, 4
category:   [Leetcode] 
tags:		[Leetcode, algorithms, math]
---

* [Leetcode 231. Power of Two](https://leetcode.com/problems/power-of-two/)

Given an integer, write a function to determine if it is a power of two.

The idea: the bit operation, only the first position is 1, others are all 0

{% highlight C++ %}
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return (n>0)&&!(n&(n-1));
    }
};
{% endhighlight %}

* [Leetcode 326. Power of Three](https://leetcode.com/problems/power-of-three/)

Given an integer, write a function to determine if it is a power of three.

The idea: use the log
{% highlight C++ %}
class Solution {
public:
    bool isPowerOfThree(int n) {
        double temp = log10(n)/log10(3);
        return temp==int(temp);
    }
};
{% endhighlight %}

* [Leetcode 342. Power of Four](https://leetcode.com/problems/power-of-four/)

Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

The idea: it must be the power of 2, and then only even position is 1
{% highlight C++ %}
class Solution {
public:
    bool isPowerOfFour(int n) {
    return (n>0) &&(!(n&n-1)) && (n-1)%3==0;
	}
};
{% endhighlight %}