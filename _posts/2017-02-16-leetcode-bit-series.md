---
layout:     post
title:      "Leetcode  (190, 191, 338, 371) Bit Series"
category:   Leetcode
tags:		Leetcode Bit
---

* content
{:toc}

Bit Series II

## Leetcode 190. Reverse Bits

* [Leetcode 190. Reverse Bits](https://leetcode.com/problems/reverse-bits/#/description)

Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).

```cpp
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        int res = 0;
        for (int i=0; i<32; i++) {
            res += n&1;
            n>>=1;
            if (i<31)   res <<=1;
        }
        return res;
    }
};
```

## Leetcode 191. Number of 1 Bits

* [Leetcode 191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/#/description)

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res = 0;
        while (n) {
            if (n%2==1) res++;
            n /=2;
        }
        return res;
    }
};
```

## Leetcode 338. Counting Bits

* [Leetcode 338. Counting Bits](https://leetcode.com/problems/counting-bits/#/description)

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:

For num = 5 you should return [0,1,1,2,1,2].

```cpp
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> res(num+1, 0);
        for (int i=1; i<=num; i++)
            res[i] = res[i>>1]+i%2;
        return res;
    }
};
```

## Leetcode 371. Sum of Two Integers

* [Leetcode 371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/#/description)

Calculate the sum of two integers a and b, but you are not allowed to use the operator `+` and `-`.

Example:

Given a = 1 and b = 2, return 3.

```cpp
class Solution {
public:
    int getSum(int a, int b) {
        int res = a^b;
        int carray = (a&b)<<1;
        if (carray!=0)  return getSum(res, carray);
        return res;
    }
};
```