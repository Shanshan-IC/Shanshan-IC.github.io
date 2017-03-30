---
layout:     post
title:      "Google APAC 2017 University Test Round D Problem A Partioning Number"
category:   Google 
tags:       Google
---
* content
{:toc}

## Problem

A and B are the only two candidates competing in a certain election. We know from polls that exactly N voters support A, and exactly M voters support B. We also know that N is greater than M, so A will win.

Voters will show up at the polling place one at a time, in an order chosen uniformly at random from all possible (N + M)! orders. After each voter casts their vote, the polling place worker will update the results and note which candidate (if any) is winning so far. (If the votes are tied, neither candidate is considered to be winning.)

What is the probability that A stays in the lead the entire time -- that is, that A will always be winning after every vote?

## Input and Output

Input

The input starts with one line containing one integer T, which is the number of test cases. Each test case consists of one line with two integers N and M: the numbers of voters supporting A and B, respectively.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is the probability that A will always be winning after every vote.

y will be considered correct if y is within an absolute or relative error of 10-6 of the correct answer. See the FAQ for an explanation of what that means, and what formats of real numbers we accept.

## Limits

1 ≤ T ≤ 100.

Small dataset

0 ≤ M < N ≤ 10.

Large dataset

0 ≤ M < N ≤ 2000.

## Sample

```
Input 
	2
	2 1
	1 0

Output 
	Case #1: 0.33333333
	Case #2: 1.00000000
```

In sample case #1, there are 3 voters. Two of them support A -- we will call them A1 and A2 -- and one of them supports B. They can come to vote in six possible orders: A1 A2 B, A2 A1 B, A1 B A2, A2 B A1, B A1 A2, B A2 A1. Only the first two of those orders guarantee that Candidate A is winning after every vote. (For example, if the order is A1 B A2, then Candidate A is winning after the first vote but tied after the second vote.) So the answer is 2/6 = 0.333333...

In sample case #2, there is only 1 voter, and that voter supports A. There is only one possible order of arrival, and A will be winning after the one and only vote.

![](/images/ML/googlecodejam2017DA.png)

## Codes

```cpp
#include <iostream>
using namespace std;

/* 扩展卡特兰数
n个1，m个0，n > m 要保证任意一个位置1的个数都大于0的个数。 
保证第一个数为1，后面n - 1个1和m个0符合扩展卡特兰数即可 
n - 1个1，m个0构成的卡特兰数的最终解为ans = C(n + m - 1, n - 1) - C(n + m - 1,n) 
*/
int main() {
    freopen("//Downloads//A-large-practice.in","r",stdin);
    freopen("//Downloads//A-large-attempt0.out","w",stdout);
    int num;
    cin >> num;
    int M, N;
    for (int i=0; i<num; i++) {
        cin >> N >> M;
        double ans = (N-M) * 1.0 / (N+M);
        cout << "Case #" << i+1 << ": " << ans << endl;
    }
    return 0;
}
```