---
layout:     post
title:      "Code Jam to I/O 2017 for Women Problem A Ticket Trouble"
category:   Google 
tags:       Google
---
* content
{:toc}

## Problem

A group of F friends is attending a conference held at an amphitheater, and they have bought tickets to see a concert there afterwards. The amphitheater is a grid of seats with S rows and S columns. For each seat, the amphitheater has sold a single ticket (although some of the tickets might not have been sold to this group of friends). Each ticket is normally labeled with a pair of integers giving the row and column numbers of one seat, in that order. For example, a ticket might normally say (2, 1), meaning row 2, column 1, or (2, 2), meaning row 2, column 2.

When the tickets were printed, there was a malfunction, and the two numbers in each pair always came out in sorted (that is, nondecreasing) order! So, for example, a ticket labeled (1, 2) might actually be for the seat in row 1, column 2, or it might actually be for the seat in row 2, column 1. If two friends have tickets labeled (1, 2), then one must actually be for row 1, column 2, and the other must actually be for row 2, column 1.

The friends will consult the box office on the day of the concert to find out what their actual seat numbers are, but for now, it is unclear! Given the printed pairs on the tickets, what is the largest possible number of the friends that could actually be seated all in the same-numbered row of seats? (The friends do not necessarily need to be seated in consecutive seats in that row.)

## Input and Output

Input

The first line of the input gives the number of test cases, T. T test cases follow. Each begins with one line with two integers F and S, representing the number of friends and the dimension of the grid of seats. Then, F more lines follow. The i-th of those lines has two integers Ai and Bi, representing the two numbers printed on the i-th friend's ticket.

Output

For each test case, output one line containing Case #x: y, where x is the test case number (starting from 1) and y is largest possible number of the friends that could actually be seated all in the same-numbered row of seats.

## Limits

F ≤ S2.

1 ≤ Ai ≤ Bi ≤ S, for all i.

No pair appears more than twice in a test case.

No pair containing the same number twice appears more than once in a test case.

Small dataset

1 ≤ T ≤ 50.

2 ≤ F ≤ 3.

2 ≤ S ≤ 3.

Large dataset

1 ≤ T ≤ 100.

2 ≤ F ≤ 100.

2 ≤ S ≤ 100.

## Sample

```
Input 
    3
    2 3
    1 2
    1 2
    3 3
    1 2
    2 3
    2 2
    3 3
    1 1
    2 2
    1 2

Output 
	Case #1: 1
    Case #2: 3
    Case #3: 2
```

In sample case #1, one ticket must actually be for row 1, column 2, and the other must actually be for row 2, column 1, even though we do not know which is which. So we know that the friends are not seated in the same row, and the largest number of friends in any row is 1. Also note that the seats have a third row and column, but none of the tickets use the third row or column.

In sample case #2, one of the tickets is definitely for seat 2 in row 2, and it is possible that two of the other tickets could be for seats 1 and 3 in row 2. So there may be as many as 3 friends in the same row.

In sample case #3, either there are two friends in row 1 and one in row 2, or there are two friends in row 2 and one in row 1. In either case, the answer is 2.

## Codes
```cpp
#include <iostream>
#include <unordered_map>

struct pair_hash {
    template <class T1, class T2>
    std::size_t operator () (const std::pair<T1,T2> &p) const {
        auto h1 = std::hash<T1>{}(p.first);
        auto h2 = std::hash<T2>{}(p.second);
        return h1 ^ h2;
    }
};

using namespace std;


int main() {
    freopen("C:\\Users\\fushanshan\\Downloads\\A-large-practice.in","r",stdin);
    freopen("C:\\Users\\fushanshan\\Downloads\\A-large-attempt0.out","w",stdout);
    int num, F, S, a, b;
    unordered_map<int, int> res;
    unordered_map<pair<int, int>, int, pair_hash> temp;
    cin >> num;
    for (int i = 0; i < num; i++) {
        cout << "Case #" << i + 1 << ": ";
        cin >> F >> S;
        for (int j = 0; j < F; j++) {
            cin >> a >> b;
            if (a == b)     res[a] += 1;
            else {
                pair<int, int> temp_P = (a > b) ? make_pair(a, b) : make_pair(b, a);
                if (temp[temp_P] == 0) {
                    res[a] += 1;
                    res[b] += 1;
                    temp[temp_P] += 1;
                }
            }

        }
        int ans = 0;
        for( int j = 1; j <= S; j++){
            if (ans < res[j])
                ans = res[j];
        }
        cout << ans << endl;
        res.clear();temp.clear();
    }
    return 0;
}
```