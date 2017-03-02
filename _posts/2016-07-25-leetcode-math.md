---
layout:     post
title:      "Leetcode  (7, 9, 11, 41, 66) Math"
category:   Leetcode 
tags:		Leetcode Math
---
* content
{:toc}

Math Questions

## Leetcode 7. Reverse Integer

* [Leetcode 7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

Reverse digits of an integer.

Example1: x = 123, return 321

Example2: x = -123, return -321

```cpp
class Solution {
public:
    int reverse(int x) {
        bool neg =false;
        long y = x;
        if (y<0)
        {
             y = -y;
             neg = true;
        }
        long res = 0;
        while (y)
        {
            res = res *10+y%10;
            y /= 10;
        }
        if (!neg && res > INT_MAX || neg && -res < INT_MIN)
            return 0;
        return (neg)?-res:res;
    }
}; 
```

## Leetcode 9. Palindrome Number

* [Leetcode 9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

Determine whether an integer is a palindrome. Do this without extra space.

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        int val = 0;
        int k = x;
        if (x<0)    return false;
        while (k) {
            int temp = k%10;
            val = val*10 + temp;
            k /= 10;
        }
        return val == x;
    }
};
```

## Leetcode 11. Container With Most Water

* [Leetcode 11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

```cpp
class Solution {
public:
    int maxArea(vector<int>& nums) {
        if (nums.empty())   return 0;
        int left = 0, right = nums.size()-1;
        int res = 0;
        while (left<right) {
            int temp = (right-left)*min(nums[left], nums[right]);
            res = max(res, temp);
            if (nums[left]<nums[right]) left++;
            else    right--;
        }
        return res;
    }
};
```

## Leetcode 66. Plus One

* [Leetcode 66. Plus One](https://leetcode.com/problems/plus-one/)

Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
       for (int i=digits.size()-1; i>=0; i--) {
           digits[i]++;
           if (digits[i]<10) break;
           digits[i] = 0;
       }
       if (digits[0]==0) {
           digits[0] = 1;
           digits.push_back(0);
       }
       return digits;
    }
};
```

## Leetcode 41. First Missing Positive

* [Leetcode 41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

Given an unsorted integer array, find the first missing positive integer.

> For example,
>
> Given [1,2,0] return 3,
>
> and [3,4,-1,1] return 2.

Your algorithm should run in O(n) time and uses constant space.

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        if (nums.empty())   return 1;
        const int n = nums.size();
        for (int i=0; i<n; i++)
            while (nums[i]>0 && nums[i]<n && nums[nums[i]-1]!=nums[i])
                swap(nums[i], nums[nums[i]-1]);
        for (int i=0; i<n; i++)
            if (nums[i] != i+1)
                return i+1;
        return n+1;
    }
};
```