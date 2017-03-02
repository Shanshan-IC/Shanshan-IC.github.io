---
layout: post
title: "Hash Theory"
category: Algorithms
tag: Hash Algorithms
---

* content
{:toc}
Hash Theory

## Hash Basic Knowledge (some from geeksforgeeks)

In computing, a hash table (hash map) is a data structure used to implement an associative array, a structure that can map keys to values. A hash table uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

1.	Suppose we want to design a system for storing employee records keyed using phone numbers. And we want following queries to be performed efficiently:

> Insert a phone number and corresponding information.
>
> Search a phone number and fetch the information.
> 
> Delete a phone number and related information.

2.	We can think of using the following data structures to maintain information about different phone numbers.

> Array of phone numbers and records.
> 
> Linked List of phone numbers and records.
> 
> Balanced binary search tree with phone numbers as keys.
>
> Direct Access Table.

3.	For arrays and linked lists, we need to search in a linear fashion, which can be costly in practice. If we use arrays and keep the data sorted, then a phone number can be searched in O(Logn) time using Binary Search, but insert and delete operations become costly as we have to maintain sorted order.

4.	With balanced binary search tree, we get moderate search, insert and delete times. All of these operations can be guaranteed to be in O(Logn) time.

5.	Hash Function: A function that converts a given big phone number to a small practical integer value. The mapped integer value is used as an index in hash table. In simple terms, a hash function maps a big number or string to a small integer that can be used as index in hash table.
A good hash function should have following properties

> Efficiently computable.
>
> Should uniformly distribute the keys (Each table position equally likely for each key)

6.	Hash Table: An array that stores pointers to records corresponding to a given phone number. An entry in hash table is NIL if no existing phone number has hash function value equal to the index for the entry.

7.	Collision Handling: Since a hash function gets us a small number for a big key, there is possibility that two keys result in same value. The situation where a newly inserted key maps to an already occupied slot in hash table is called collision and must be handled using some collision handling technique. Following are the ways to handle collisions:
	
> Chaining:The idea is to make each cell of hash table point to a linked list of records that have same hash function value. Chaining is simple, but requires additional memory outside the table.
>
> Open Addressing: In open addressing, all elements are stored in the hash table itself. Each table entry contains either a record or NIL. When searching for an element, we one by one examine table slots until the desired element is found or it is clear that the element is not in the table.

8. Hash Load Factor: numbers of elements in hash table / table size
