---
layout:     post
title:      "Leetcode (121, 122, 123) Best Time to Buy and Sell Stock"
category:   Leetcode 
tags:       Leetcode ListNode
---

* content
{:toc}
Best Time to Buy and Sell Stock

## Leetcode 121. Best Time to Buy and Sell Stock

* [Leetcode 121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:

> Input: [7, 1, 5, 3, 6, 4]
> 
> Output: 5
> 
> max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)

Example 2:
	
> Input: [7, 6, 4, 3, 1]
> 
> Output: 0

In this case, no transaction is done, i.e. max profit = 0.

```cpp
class Solution {
public:
    int maxProfit(vector<int>& nums) {
        if (nums.empty())   return 0;
        int res = 0, minP = INT_MAX;
        for (int p:nums) {
            minP = min(p, minP);
            res = max(res, p-minP);
        }
        return res;
    }
};
```

## Leetcode 122. Best Time to Buy and Sell Stock II

* [Leetcode 122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

```cpp
class Solution {
public:
    int maxProfit(vector<int>& nums) {
        int res = 0, minP = INT_MAX;
        if (nums.empty())   return 0;
        for (int p:nums) {
            if (p>minP) res+=p-minP;
            minP = p;
        }
        return res;
    }
};
```

## Leetcode 123. Best Time to Buy and Sell Stock III

* [Leetcode 123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        const int n = prices.size();
        if (n<2)    return 0;
        vector<int> preProfits(n, 0);
        vector<int> postProfits(n, 0);
        int minP = prices[0];
        for (int i=1; i<n; i++) {
            minP = min(minP, prices[i]);
            preProfits[i] = max(preProfits[i-1], prices[i]-minP);
        }
        int maxP = prices[n-1];
        for (int i=n-2; i>=0; i--) {
            maxP = max(maxP, prices[i]);
            postProfits[i] = max(postProfits[i+1], maxP-prices[i]);
        }
        int res = 0;
        for (int i=0; i<n; i++)
            res = max(res, preProfits[i]+postProfits[i]);
        return res;
    }
};
```