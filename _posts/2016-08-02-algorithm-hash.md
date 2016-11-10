---
layout: post
title: Hash
category: Algorithms
tag: [hash, algorithms]
---

Hash Basic Knowledge (some from geeksforgeeks)

In computing, a hash table (hash map) is a data structure used to implement an associative array, a structure that can map keys to values. A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

1.	Suppose we want to design a system for storing employee records keyed using phone numbers. And we want following queries to be performed efficiently:

	Insert a phone number and corresponding information.

	Search a phone number and fetch the information.

	Delete a phone number and related information.

2.	We can think of using the following data structures to maintain information about different phone numbers.

	Array of phone numbers and records.

	Linked List of phone numbers and records.

	Balanced binary search tree with phone numbers as keys.
	
	Direct Access Table.

3.	For arrays and linked lists, we need to search in a linear fashion, which can be costly in practice. If we use arrays and keep the data sorted, then a phone number can be searched in O(Logn) time using Binary Search, but insert and delete operations become costly as we have to maintain sorted order.

4.	With balanced binary search tree, we get moderate search, insert and delete times. All of these operations can be guaranteed to be in O(Logn) time.

5.	Hash Function: A function that converts a given big phone number to a small practical integer value. The mapped integer value is used as an index in hash table. In simple terms, a hash function maps a big number or string to a small integer that can be used as index in hash table.
A good hash function should have following properties

1) Efficiently computable.

2) Should uniformly distribute the keys (Each table position equally likely for each key)

6.	Hash Table: An array that stores pointers to records corresponding to a given phone number. An entry in hash table is NIL if no existing phone number has hash function value equal to the index for the entry.

7.	Collision Handling: Since a hash function gets us a small number for a big key, there is possibility that two keys result in same value. The situation where a newly inserted key maps to an already occupied slot in hash table is called collision and must be handled using some collision handling technique. Following are the ways to handle collisions:

Chaining:The idea is to make each cell of hash table point to a linked list of records that have same hash function value. Chaining is simple, but requires additional memory outside the table.

Open Addressing: In open addressing, all elements are stored in the hash table itself. Each table entry contains either a record or NIL. When searching for an element, we one by one examine table slots until the desired element is found or it is clear that the element is not in the table.

Re-hash

8. Hash Load Factor: numbers of elements in hash table / table size


A related baidu interview question

百度：

搜索引擎会通过日志文件把用户每次检索使用的所有检索串都记录下来，每个查询串的长度为1-255字节。假设目前有一千万个记录（这些查询串的重复度比较高，虽然总数是1千万，但如果除去重复后，不超过3百万个。一个查询串的重复度越高，说明查询它的用户越多，也就是越热门。），请你统计最热门的10个查询串，要求使用的内存不能超过1G。

即，此问题的解决分为以下两个步骤：
　　第一步：Query统计
　　Query统计有以下俩个方法，可供选择：
　　1、直接排序法
　　首先我们最先想到的的算法就是排序了，首先对这个日志里面的所有Query都进行排序，然后再遍历排好序的Query，统计每个Query出现的次数了。
　　但是题目中有明确要求，那就是内存不能超过1G，一千万条记录，每条记录是255Byte，很显然要占据2.375G内存，这个条件就不满足要求了
让我们回忆一下数据结构课程上的内容，当数据量比较大而且内存无法装下的时候，我们可以采用外排序的方法来进行排序，这里我们可以采用归并排序，因为归并排序有一个比较好的时间复杂度O(nlogn)。
　　排完序之后我们再对已经有序的Query文件进行遍历，统计每个Query出现的次数，再次写入文件中。
　　综合分析一下，排序的时间复杂度是O(nlogn)，而遍历的时间复杂度是O(n)，因此该算法的总体时间复杂度就是O(n+nlogn)=O(nlogn)。
2. hash table
因为Hash Table的查询速度非常的快，几乎是O(1)的时间复杂度。
　　那么，我们的算法就有了：维护一个Key为Query字串，Value为该Query出现次数的HashTable，每次读取一个Query，如果该字串不在Table中，那么加入该字串，并且将Value值设为1；如果该字串在Table中，那么将该字串的计数加一即可。最终我们在O(n)的时间复杂度内完成了对该海量数据的处理。
　　本方法相比算法1：在时间复杂度上提高了一个数量级，为O(n)，但不仅仅是时间复杂度上的优化，该方法只需要IO数据文件一次，而算法1的IO次数较多的，因此该算法2比算法1在工程上有更好的可操作性。
　　第二步：找出Top 10
　　算法一：普通排序
    我想对于排序算法大家都已经不陌生了，这里不在赘述，我们要注意的是排序算法的时间复杂度是O(nlogn)，在本题目中，三百万条记录，用1G内存是可以存下的。
　　算法二：部分排序
　　题目要求是求出Top 10，因此我们没有必要对所有的Query都进行排序，我们只需要维护一个10个大小的数组，初始化放入10个Query，按照每个Query的统计次数由大到小排序，然后遍历这300万条记录，每读一条记录就和数组最后一个Query对比，如果小于这个Query，那么继续遍历，否则，将数组中最后一条数据淘汰，加入当前的Query。最后当所有的数据都遍历完毕之后，那么这个数组中的10个Query便是我们要找的Top10了。
　　不难分析出，这样，算法的最坏时间复杂度是N*K， 其中K是指top多少。
　　算法三：堆
　　在算法二中，我们已经将时间复杂度由NlogN优化到NK，不得不说这是一个比较大的改进了，可是有没有更好的办法呢？
　　分析一下，在算法二中，每次比较完成之后，需要的操作复杂度都是K，因为要把元素插入到一个线性表之中，而且采用的是顺序比较。这里我们注意一下，该数组是有序的，一次我们每次查找的时候可以采用二分的方法查找，这样操作的复杂度就降到了logK，可是，随之而来的问题就是数据移动，因为移动数据次数增多了。不过，这个算法还是比算法二有了改进。
