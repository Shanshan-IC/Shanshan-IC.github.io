---
layout:     post
title:      Google CodeJam ProblemE B Beautiful Numbers
category:   [Google] 
tags:       [Google]
---

Problem

We consider a number to be beautiful if it consists only of the digit 1 repeated one or more times. Not all numbers are beautiful, but we can make any base 10 positive integer beautiful by writing it in another base.

Given an integer N, can you find a base B (with B > 1) to write it in such that all of its digits become 1? If there are multiple bases that satisfy this property, choose the one that maximizes the number of 1 digits.

Input

The first line of the input gives the number of test cases, T. T test cases follow. Each test case consists of one line with an integer N.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is the base described in the problem statement.

Limits

1 ≤ T ≤ 100.

Small dataset

3 ≤ N ≤ 1000.

Large dataset

3 ≤ N ≤ 1018.

Sample

Input 
 
	2
	3
	13

Output 

	Case #1: 2
	Case #2: 3

In case #1, the optimal solution is to write 3 as 11 in base 2.

In case #2, the optimal solution is to write 13 as 111 in base 3. Note that we could also write 13 as 11 in base 12, but neither of those representations has as many 1s.

{% highlight C++ %}
#include <iostream>
#include <cmath>
using namespace std;

bool isvalid(long long num, long long j) {
    while (num) {
        if (num % j != 1)   return false;
        num /= j;
    }
    return true;
}
int main() {
    freopen("//Downloads//B-large-practice.in","r",stdin);
    freopen("//Downloads//B-large-attempt0.out","w",stdout);
    int N;
    cin >> N;
    long long num;
    for (int i=0; i<N; i++) {
        cin >> num;
        // long long half = sqrt(num);
        for (long long j=2; j<=num; j++) {
            if (isvalid(num, j)) {
                cout << "Case #" << i+1 << ": " << j << endl;
                break;
            }
        }
    }
    return 0;
}
{% endhighlight %}