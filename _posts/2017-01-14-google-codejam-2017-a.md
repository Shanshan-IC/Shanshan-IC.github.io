---
layout:     post
title:      "Google CodeJam Round E 2017 Problem A Diwali lightings"
category:   Google 
tags:       Google
---
* content
{:toc}

## Problem

Diwali is the festival of lights. To celebrate it, people decorate their houses with multi-color lights and burst crackers. Everyone loves Diwali, and so does Pari. Pari is very fond of lights, and has transfinite powers, so she buys an infinite number of red and blue light bulbs. As a programmer, she also loves patterns, so she arranges her lights by infinitely repeating a given finite pattern S.

For example, if S is BBRB, the infinite sequence Pari builds would be BBRBBBRBBBRB...

Blue is Pari's favorite color, so she wants to know the number of blue bulbs between the Ith bulb and Jth bulb, inclusive, in the infinite sequence she built (lights are numbered with consecutive integers starting from 1). In the sequence above, the indices would be numbered as follows:

```
	B  B  R  B  B  B  R  B  B  B  R  B...
	1  2  3  4  5  6  7  8  9  10 11 12
```

So, for example, there are 4 blue lights between the 4th and 8th positions, but only 2 between the 10th and 12th.

Since the sequence can be very long, she wrote a program to do the count for her. Can you do the same?

## Input and Output

Input

The first line of the input gives the number of test cases, T. T test cases follow.

First line of each test case consists of a string S, denoting the initial finite pattern.

Second line of each test case consists of two space separated integers I and J, defined above.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is number of blue bulbs between the Ith bulb and Jth bulb of Pari's infinite sequence, inclusive.

## Limits

1 ≤ T ≤ 100.

1 ≤ length of S ≤ 100.

Each character of S is either uppercase B or uppercase R.

Small dataset

1 ≤ I ≤ J ≤ 106.

Large dataset

1 ≤ I ≤ J ≤ 1018.

## Sample
```
Input 
 
    3
    BBRB
    4 8
    BBRB
    10 12
    BR
    1 1000000

Output 

    Case #1: 4
    Case #2: 2
    Case #3: 500000
```

## Codes

```cpp
#include <iostream>
#include <fstream>
#define LL long long 
using namespace std;

void countF(string pattern, LL left, LL right) {
    int len = pattern.size();
    LL l1 = left / len, l2 = left % len;
    LL r1 = right / len, r2 = right % len;
    LL count = 0, ll = 0, rr = 0;
    for (int i=0; i<len; i++) {
        if (pattern[i] == 'B')  count++;
        if (i+1 == l2)  ll = count;
        if (i+1 == r2)  rr = count;
    }
    LL sum1 = r1*count+rr;
    LL sum2 = l1*count+ll;
    cout << sum1 - sum2 << endl;
}

int main() {
    int N;
    LL left, right;
    freopen("//Downloads//A-large-practice.in","r",stdin);
    freopen("//Downloads//A-large-attempt0.out","w",stdout);
    cin >> N;
    string pattern;
    for (int i=0; i<N; i++) {
        cin >> pattern;
        cin >> left >> right;
        printf("Case #%d: ",i+1);
        countF(pattern, left-1, right);

    }
    return 0;
}
```