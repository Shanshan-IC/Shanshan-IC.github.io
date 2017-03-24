---
layout:     post
title:      "Leetcode (72) Edit Distance"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

## Leetcode 72. Edit Distance

[Leetcode 72. Edit Distance](https://leetcode.com/problems/edit-distance/)

Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

a) Insert a character
b) Delete a character
c) Replace a character

The idea is from [blog](http://blog.csdn.net/feliciafay/article/details/17502919)

本题是典型的适合使用动态规划的题目。在斯坦福的公开课(中文，英文)上，有对这个问题的详细说明，所以接下来就继续使用斯坦福公开课的例子了。
如果要计算单词"INTENTION"和单词"EXECUTION"之间的编辑距离，那么该怎么计算呢？
首先，把这个问题简单化。把上面两个单词简化为长度为1的两个单词I和E。
如果要“I”变化为"E"，可以把"I"替换为"E"
如果要“I”变化为空串" "，可以把"I"删除，从而形成""
如果要空串“ ”变化为"E"，可以把"E"插入，从而形成E
上面三种变化分别表示替换，删除，插入这三种基本操作。
接下来，定义一个表达式D(i,j)。它表示从第1个字单词的第0位至第i位形成的子串和第2个单词的第0位至第j位形成的子串的编辑距离。
显然，可以计算出动态规划的初始表达式，如下:
D(i,0) = i
D(0,j) = j
然后，考虑动态规划的状态转移方程式，如下:
                                   D(i-1, j) + 1
D(i,j)=min                  ( D(i, j-1) + 1 )
                                   D(i-1, j-1) +2( if  X(i) != Y(j) ) ; D(i-1,j-1) ( if  X(i) == Y(j) )
上面的状态转移方程的含义是，D(i,j)的值，要么是D(i-1, j)的操作完成之后删除一个字符(第1个单词的第i个字符)，要么是D(i, j-1)的操作完成之后增加一个字符(第2个单词的第j个字符)，要么是D(i-1, j-1)的操作完成自后替换一个字符(如果第1个单词的第i个字符和第2个单词的第j个字符不等)，或者是D(i-1, j-1)的操作完成自后什么也不做(如果第1个单词的第i个字符和第2个单词的第j个字符相等)。其中，课件定义删除，插入，替换的操作步数分别为一步，一步，两步。

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        const int l1 = word1.size();
        const int l2 = word2.size();
        vector<vector<int>> dp(l1+1, vector<int>(l2+1, 0));
        for (int i=1; i<=l1; i++)
            dp[i][0] = i;
        for (int j=1; j<=l2; j++)
            dp[0][j] = j;
        for (int i=1; i<=l1; i++)
            for (int j=1; j<=l2; j++){
                dp[i][j]= min(dp[i-1][j]+1, dp[i][j-1]+1);
                if (word1[i-1] != word2[j-1])
                    dp[i][j] = min(dp[i][j], dp[i-1][j-1]+1);
                else
                    dp[i][j] = min(dp[i][j], dp[i-1][j-1]);
            }
        return dp[l1][l2];
    }
};
```