---
layout:     post
title:      Algorithm array and string
category:   [Algorithms] 
tags:		[Algorithms, String, Array]
---

* Array
{% highlight C++ %}
// define array in the stack
int array[arraySize];
// define array in the heap
int *array = new int[arraySize];
// free the memory after using it
delete[] array;
{% endhighlight %}
Array can be accessed by index, so modify and read an element, O(1).
Delete and Insert elements needs to move the later elements, O(N).

* Stack and Heap

栈主要是指由操作系统自动管理的内存空间。当进入一个函数，操作系统会为该函数中的局部变量分配存储空间。事实上，系统会分配一个内存块，叠加在当前的栈上，并且利用指针指向前一个内存块的地址。函数的局部变量就存储在当前的内存块上。当该函数返回时，系统“弹出”内存块，并且根据指针回到前一个内存块。所以，栈总是以后进先出(LIFO)的方式工作。通常，在栈上分配的空间不需要用户操心。

堆是用来存储动态分配变量的空间。对于堆而言，并没有像栈那样后进先出的规则，程序员可以选择随时分配或回收内存。这就意味着需要程序员自己用命令回收内存，否则会产生内存泄漏(memory leak)。在C/C++中，程序员需要调用free/delete来释放动态分配的内存。

* String

Some string functions used frequently
{% highlight C++ %}
string str ("This is a string");
int length = str.length();    // length equals to 16
str.erase(0,10);    // str becomes "string", with length 6 after erasure
string subStr = str.substr(10,6);    // subStr equals to "string", with length 6
{% endhighlight %}

* String Matching Algorithms

Brute-Force算法： 顺序遍历母串，将每个字符作为匹配的起始字符，判断是否匹配子串。时间复杂度 O(mn)。

Rabin-Karp算法：将每一个匹配子串映射为一个哈希值。例如，将子串看做一个多进制数，比较它的值与母串中相同长度子串的哈希值，如果相同，再细致地按字符确认字符串是否确实相同。顺序计算母串哈希值的过程中，使用增量计算的方法：扣除最高位的哈希值，增加最低位的哈希值。因此能在平均情况下做到O(m+n)。
