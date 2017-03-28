---
layout:     post
title:      "Google Code Jam Round 1B 2016 A. Getting the Digits"
category:   Google
tags:       Google
---

* content
{:toc}

## Problem

You just made a new friend at an international puzzle conference, and you asked for a way to keep in touch. You found the following note slipped under your hotel room door the next day:

"Salutations, new friend! I have replaced every digit of my phone number with its spelled-out uppercase English representation ("ZERO", "ONE", "TWO", "THREE", "FOUR", "FIVE", "SIX", "SEVEN", "EIGHT", "NINE" for the digits 0 through 9, in that order), and then reordered all of those letters in some way to produce a string S. It's up to you to use S to figure out how many digits are in my phone number and what those digits are, but I will tell you that my phone number consists of those digits in nondecreasing order. Give me a call... if you can!"

You would to like to call your friend to tell him that this is an obnoxious way to give someone a phone number, but you need the phone number to do that! What is it?

## Input and Output

Input

The first line of the input gives the number of test cases, T. T test cases follow. Each consists of one line with a string S of uppercase English letters.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is a string of digits: the phone number.

## Limits

1 ≤ T ≤ 100.

A unique answer is guaranteed to exist.

Small dataset

3 ≤ length of S ≤ 20.

Large dataset

3 ≤ length of S ≤ 2000.

## Sample

```
Input 

    4
    OZONETOWER
    WEIGHFOXTOURIST
    OURNEONFOE
    ETHER

Output 

    Case #1: 012
    Case #2: 2468
    Case #3: 114
    Case #4: 3
`

## Codes

```cpp
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;

int main() {
    freopen("C:\\Users\\Administrator\\Downloads\\A-small-practice.in","r",stdin);
    freopen("C:\\Users\\Administrator\\Downloads\\A-small-attempt0.out","w",stdout);
    string a[] = {"ZERO", "ONE", "TWO", "THREE", "FOUR", "FIVE", "SIX", "SEVEN", "EIGHT", "NINE"};
    string ordered[] = {"0", "2", "4", "6", "8", "3", "5", "1", "7", "9"};
    string t = "ZWUXGHFOVI";
    int num;
    cin >> num;
    string str;
    for (int i = 0; i < num; i++) {
        string res = "";
        cout << "Case #" << i + 1 << ": ";
        cin >> str;
        int map[26] = {0};
        for (int i = 0; i<str.size(); i++)
            map[(int)(str[i]-'A')]++;
        for (int i = 0; i < 10; i++) {
            while (map[(int)(t[i]-'A')]) {
                res += ordered[i];
                int temp = stoi(ordered[i]);
                for (int j = 0; j < a[temp].size(); j++)
                    map[(int)a[temp][j]-'A']--;
            }
        }
        sort(res.begin(), res.end());
        cout << res << endl;
    }
    return 0;
}
```