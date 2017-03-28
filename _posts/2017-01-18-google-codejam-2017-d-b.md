---
layout:     post
title:      "Google CodeJam Round D 2017 Problem B Sitting"
category:   Google 
tags:       Google
---
* content
{:toc}

## Problem

The Codejamon game is on fire! Many players have gathered in an auditorium to fight for the World Championship. At the opening ceremony, players will sit in a grid of seats with R rows and C columns.

The competition will be intense, and the players are sensitive about sitting near too many of their future opponents! A player will feel too crowded if another player is seated directly to their left and another player is seated directly to their right. Also, a player will feel too crowded if one player is seated directly in front of them and another player is seated directly behind them. 

What is the maximum number of players that can be seated such that no player feels too crowded? 

## Input and Output

Input

The first line of the input gives the number of test cases, T. T test cases follow. Each test case consists of one line with two integers R and C: the number of rows and columns of chairs in the auditorium.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is the maximum number of players that can be seated, as described in the problem statement.

## Limits

1 ≤ T ≤ 100.

Small dataset

1 ≤ R ≤ 5.

1 ≤ C ≤ 5.

Large dataset

1 ≤ R ≤ 100.

1 ≤ C ≤ 100.

## Sample

```
Input 
	3
	2 2
	2 3
	4 1

Output 
	Case #1: 4
	Case #2: 4
	Case #3: 3
```
In sample case #1, we can fill all seats, and no player will feel too crowded.

In sample case #2, each row has three seats. We can't put three players in a row, since that would make the middle player feel too crowded. One optimal solution is to fill each of the first two columns, for a total of four players.

In sample case #3, one optimal solution is to fill the first two rows and the last row, for a total of three players.

The idea is from [http://blog.csdn.net/dumeichen/article/details/52916711](http://blog.csdn.net/dumeichen/article/details/52916711)

## Codes
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

/*
for one row, the maximum numbers are m - m/3
for three rows, the maximum numbers are 2*m
for n (n>3) rows, the first row has to be k = m-m/3
n/3 use 2*m the ways to fill in
n%3
if there still is one row, fill in m-m/3
if there still are two rows, the rules are:
consider the relationship between m%3 and the numbers of every row
1. the first row has to be k = m-m/3
2. when m%3==0, three rows numbers must be k, k, k
   when m%3==1, three rows numbers must be k, k, k-1
   when m%3==2, three rows numbers must be k, k-1, k-1
so if m%3!= 2, the two rows both must be filled in k and k, otherwise it should be k and k-1
*/
int main() {
    freopen("//Downloads//B-small-practice.in","r",stdin);
    freopen("//Downloads//B-small-attempt0.out","w",stdout);
    int num;
    cin >> num;
    int m, n;
    for (int i=0; i<num; i++) {
        cin >> n >> m;
        int res=0;
        if (n>m)    swap(n, m);
        int k = m - m/3;    // the maximum numbers in one row
        res += n/3 * 2 * m;
        int temp = n%3;
        if (temp==1)    res += k;
        else if (temp==2) {
            if (m%3==2 && n>3) res = res+(k+k-1);
            else    res = res+2*k;
        }
        cout << "Case #" << i+1 << ": " << res << endl;
    }
    return 0;
}
```