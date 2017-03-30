---
layout:     post
title:      "Google APAC 2017 University Test Round E Problem C Partioning Number"
category:   Google 
tags:       Google
---
* content
{:toc}

## Problem

Shekhu has N balls. She wants to distribute them among one or more buckets in a way that satisfies all of these constraints:

The numbers of balls in the buckets must be in non-decreasing order when read from left to right.

The leftmost bucket must be non-empty and the number of balls in the leftmost bucket must be divisible by D.

The difference (in number of balls) between any two buckets (not just any two adjacent buckets) must be less than or equal to 2.

How many different ways are there for Shekhu to do this? Two ways are considered different if the lists of numbers of balls in buckets, reading left to right, are different.

## Input and Output
Input

The first line of the input gives the number of test cases, T.
T test cases follow. Each test case consists of one line with two integers N and D, as described above.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is the answer, as described above.

## Limits

1 ≤ T ≤ 100.

1 ≤ D ≤ 100.

Small dataset

1 ≤ N ≤ 2000.

Large dataset

1 ≤ N ≤ 100000.

## Sample

```
Input 

	3
	7 1
	7 2
	2 4

Output 

	Case #1: 10
	Case #2: 1
	Case #3: 0

In sample case #1, the possible distributions are:

	1 1 1 1 1 1 1
	1 1 1 1 1 2
	1 1 1 1 3
	1 1 1 2 2
	1 2 2 2
	1 1 2 3
	1 3 3
	2 2 3
	3 4
	7
```

Note that 1 2 4 is not a valid distribution, since the difference between 1 and 4 is more than 2.

In sample case #2, the possible distributions are:

2 2 3

3 4 is not possible, since the first term is not divisible by 2.

In sample case #3, no possible arrangement exists.

## Codes
```cpp
#include <iostream>
using namespace std;

long long getPartioning(int num, int d) {
    long long res = 0;
    int i,k,m,l,r;
    for (i=d; i<num; i+=d)
        for (k=(num-1-i)/(i+2)+2; k<=num/i; k++) {
            m = num-k*i;
            l = m-k+1;  if (l<0)   l=0;
            r = m/2;    if (r>k-1)  r=k-1;
            if (l<=r)   res+=(r-l+1);
        }
    if (num%d ==0)  res++;
    return res;    
}
int main() {
    freopen("//Downloads//C-small-practice.in","r",stdin);
    freopen("//Downloads//C-small-attempt0.out","w",stdout);
    int N;
    cin >> N;
    int num, d;
    for (int i=0; i<N; i++) {
        cin >> num >> d;
        cout << "Case #" << i+1 << ": " << getPartioning(num, d) << endl;
    }
    return 0;
}
```