---
layout:     post
title:      "Leetcode (53, 91, 97, 152) Dynamic Programming"
category:   Leetcode
tags:		Leetcode DP
---

* content
{:toc}

Dynamic Programming in Leetcode

## Leetcode 53. Maximum Subarray

[Leetcode 53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray)

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

Idea: The formula should should be 
**sum[i] = max{A[i], A[i] + sum[i+1]}**

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        const int n = nums.size();
        int res[n] = {0};
        res[0] = nums[0];   
        int maxs = nums[0];
        for (int i=1; i<n; i++) 
            res[i] = max(nums[i], res[i-1]+nums[i]);
        for (int i=1; i<n; i++) 
            maxs = max(maxs, res[i]);
        return maxs;
    }
};
```

## Leetcode 91. Decode Ways

[Leetcode 91. Decode Ways](https://leetcode.com/problems/decode-ways/#/description)

A message containing letters from A-Z is being encoded to numbers using the following mapping:

`
'A' -> 1
'B' -> 2
...
'Z' -> 26
`

Given an encoded message containing digits, determine the total number of ways to decode it.

For example,

Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.

idea:

动态规划，令dp[i]表示字符串的前i个字符的可能的编码方式的数量。那么递推公式如下：

如果当前数字为0，则前面数字必为1或者2，否则无法进行编码转换，此时的数字0只能和前面的1或者2连在一起进行编码，因此dp[i] = dp[i-2]；
如果前面数字为1或者前面数字为2且当前数字在1~6之间，说明都可以进行2种编码（分开或者和在一起），因此dp[i] = dp[i-1] + dp[i-2]；
其他情况，当前数字必须单独进行编码转换，因此dp[i] = dp[i-1]。

```cpp
class Solution {
public:
    int numDecodings(string s) {
        const int n = s.size();
        if (n==0 || s[0]=='0')   return 0;
        vector<int>dp(n+1, 0);
        dp[0] = 1;dp[1] = 1;
        for (int i=2; i<=n; i++) {
            if (s[i-1]!='0')  dp[i] = dp[i-1];
            if (s[i-2]=='1'|| (s[i-2]=='2' && s[i-1]>'0' && s[i-1]<'7'))
                dp[i] += dp[i-2];
            if (s[i-1]=='0' &&(s[i-2]=='1'||s[i-2]=='2'))
                dp[i] = dp[i-2];
        }
        return dp[n];
    }
};
```

## Leetcode 97. Interleaving String

[Leetcode 97. Interleaving String](https://leetcode.com/problems/interleaving-string/#/description)

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

For example,

Given:

s1 = "aabcc",

s2 = "dbbca",

When s3 = "aadbbcbcac", return true.

When s3 = "aadbbbaccc", return false.

The idea is from [blog](http://www.cnblogs.com/ganganloveu/p/4137843.html)

s1, s2只有两个字符串，因此可以展平为一个二维地图，判断是否能从左上角走到右下角。

当s1到达第i个元素，s2到达第j个元素:

地图上往右一步就是s2[j-1]匹配s3[i+j-1]。

地图上往下一步就是s1[i-1]匹配s3[i+j-1]。

示例：s1="aa",s2="ab",s3="aaba"。标1的为可行。最终返回右下角。

`
     0  a  b

0   1  1  0

a   1  1  1

a   1  0  1
`

```cpp
class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        const int n = s1.size();
        const int m = s2.size();
        const int p = s3.size();
        if (n+m != p)   return false;
        vector<vector<bool>> res(n+1, vector<bool>(m+1, false));
        for (int i=0; i<n+1; i++)
            for (int j=0; j<m+1; j++) {
                if (i==0 && j==0)   res[i][j]=true;
                else if (i==0)   res[i][j] = res[i][j-1] & (s2[j-1]==s3[j-1]);
                else if (j==0)  res[i][j] = res[i-1][j] & (s1[i-1]==s3[i-1]);
                else    res[i][j] = (res[i-1][j] & (s1[i-1]==s3[i+j-1])) || (res[i][j-1] & (s2[j-1]==s3[i+j-1]));
            } 
        return res[n][m];
    }
};
```

## Leetcode 152. Maximum Product Subarray Add to List


[Leetcode 152. Maximum Product Subarray Add to List](https://leetcode.com/problems/maximum-product-subarray/#/description)

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxP = 1, minP = 1, res = INT_MIN;
        for (int num: nums) {
            int temp = maxP;
            maxP = max(max(maxP*num, minP*num), num);
            minP = min(min(minP*num, temp*num), num);
            res = max(res, maxP);
        }
        return res;
    }
};
```