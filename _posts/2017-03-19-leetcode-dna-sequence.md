---
layout:     post
title:      "Leetcode 187 Repeated DNA Sequences"
category:   Leetcode
tags:		Leetcode Bit
---

* content
{:toc}

## Leetcode 187. Repeated DNA Sequences

[Leetcode 187. Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/#/description)

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

For example,

`
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
`

思路：将字符串中所有长度为10的子串以及出现的次数用map保存，但是需要消耗很大的空间。

考虑到只有4中可能的字符A,C,G,T;可以对字符进行编码，用2bit来表示一个字符，一个含有10个字符的子串只要20bit就能表示，用一个int类型就能表示。

总长度为n的字符串，可能的子串共有n-9种，因此最多用n-9个int就能表示所有的字符组合。最坏的情况下，20bit共有2^20中组合，即1024*1024，

一个int类型4byte,因此额外消耗4MB的二外空间。

`
A : 0100 0001
C : 0100 0011
G : 0100 0111
T : 0101 0100
`

Only the last three bits are different.

```cpp
class Solution {
public:
    // A65 C67 G71 T84 
    vector<string> findRepeatedDnaSequences(string s) {
        vector<string> res;
        unordered_map<int,int> table;
        const int n = s.size();
        int curr = 0;
        for(int i = 0; i < n; i++){
            curr <<= 3; //shift left 3
            curr |= (s[i]&7);  //Only the last three bits are different.
            curr &= 0x3FFFFFFF;
            if(i >= 9 && ++table[curr] == 2) res.push_back(s.substr(i-9,10));
        }
        return res;
    }
};
```