---
layout:     post
title:      "Algorithm array and string"
category:   Algorithms
tags:		Algorithms String Array
---

* content
{:toc}
String and Array

## Array

```cpp
// define array in the stack
int array[arraySize];
// define array in the heap
int *array = new int[arraySize];
// free the memory after using it
delete[] array;
```

Array can be accessed by index, so modify and read an element, O(1).
Delete and Insert elements needs to move the later elements, O(N).

## String

Some string functions used frequently

```cpp
string str ("This is a string");
int length = str.length();    // length equals to 16
str.erase(0,10);    // str becomes "string", with length 6 after erasure
string subStr = str.substr(10,6);    // subStr equals to "string", with length 6
```

## String Matching Algorithms

Brute-Force算法： 顺序遍历母串，将每个字符作为匹配的起始字符，判断是否匹配子串。时间复杂度 O(mn)。

Rabin-Karp算法：将每一个匹配子串映射为一个哈希值。例如，将子串看做一个多进制数，比较它的值与母串中相同长度子串的哈希值，如果相同，再细致地按字符确认字符串是否确实相同。顺序计算母串哈希值的过程中，使用增量计算的方法：扣除最高位的哈希值，增加最低位的哈希值。因此能在平均情况下做到O(m+n)。
