---
layout:     post
title:      Leetcode  (4, 50, 172, 204)	Math Series	
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Math]
---

* [Leetcode 4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

	Example 1:
	nums1 = [1, 3]
	nums2 = [2]

	The median is 2.0
	Example 2:
	nums1 = [1, 2]
	nums2 = [3, 4]
	The median is (2 + 3)/2 = 2.5

{% highlight C++ %}
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        const int m = nums1.size();
        const int n = nums2.size();
        int k = (m+n)/2;
        if ((m+n)%2!=0)
            return helper(nums1, nums2, k+1);
        else
            return (helper(nums1, nums2, k) + helper(nums1, nums2, k+1))/2;
    }
    
    double helper(vector<int> &nums1, vector<int> &nums2, int k) {
        const int m = nums1.size();
        const int n = nums2.size();
        if (m>n)    return helper(nums2, nums1, k);
        if (m==0)   return nums2[k-1];
        if (k==1)   return min(nums1[0], nums2[0]);
        
        int pa = min(m, k/2), pb = k-pa;
        if (nums1[pa-1] < nums2[pb-1]) {
            vector<int> a(nums1.begin()+pa, nums1.end());
            return helper(a, nums2, k-pa);
        }
        else {
            vector<int> b(nums2.begin()+pb, nums2.end());
            return helper(nums1, b, k-pb);
        }
        
    }
};
{% endhighlight %}

* [Leetcode 50. Pow(x, n)](https://leetcode.com/problems/powx-n/)

Implement pow(x, n).

{% highlight C++ %}
class Solution {
public:
    double myPow(double x, int n) {
        if (n==0)   return 1;
        if (x==0)   return 0;
        if (n>0)    return helper(x, n);
        else    return helper(1/x, -n);
    }
    
    double helper(double x, int n) {
        if (n==0)   return 1;
        double half = helper(x, n/2);
        if (n%2==0)
            return half*half;
        else
            return half*half*x;
    }
};
{% endhighlight %}

*  [Leetcode 172. Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes/)

Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.

{% highlight C++ %}
class Solution {
public:
    int trailingZeroes(int n) {
        int count = 0;
        while (n) {
            count += n/5;
            n /= 5;
        }
        return count;
    }
};
{% endhighlight %}

*  [Leetcode 204. Count Primes](https://leetcode.com/problems/count-primes/)

Count the number of prime numbers less than a non-negative number, n.

{% highlight C++ %}
class Solution {
public:
    int countPrimes(int n) {
        vector<int> p(n, 1);
        int ans = 0;
        for (int i=2; i<n; i++) {
            ans += p[i];
            if (p[i]==1)
                for (int j=i; j<n; j+=i)
                    p[j] = 0;
        }
        return ans;
    }
};
{% endhighlight %}