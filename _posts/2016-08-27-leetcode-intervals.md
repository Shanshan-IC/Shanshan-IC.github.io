---
layout:     post
title:      "Leetcode (56, 57) Merge Intervals and Insert Intervals"
category:   Leetcode 
tags:		Leetcode
---

* content
{:toc}

## Intervals structure

```cpp
struct Interval {
    int start;
    int end;
    Interval() : start(0), end(0) {}
    Interval(int s, int e) : start(s), end(e) {}
 };
```

## Leetcode 56. Merge Intervals

* [Leetcode 56. Merge Intervals](https://oj.leetcode.com/problems/merge-intervals/)

Given a collection of intervals, merge all overlapping intervals.

> For example,
>
> Given [1,3],[2,6],[8,10],[15,18],
>
> return [1,6],[8,10],[15,18].

```cpp
class Solution {
public:
    vector<Interval> merge(vector<Interval>& intervals) {
        vector<Interval> res;
        if (intervals.empty())  return res;
        sort(intervals.begin(), intervals.end(), [](Interval &i, Interval &j){return i.start<j.start;});
        const int n = intervals.size();
        for (int i=0; i<n; i++) {
            if (i+1<n && intervals[i+1].start<=intervals[i].end) {
                intervals[i+1].end = max(intervals[i].end, intervals[i+1].end);
                intervals[i+1].start = min(intervals[i].start, intervals[i+1].start);
            }
            else
                res.push_back(intervals[i]);
        }
        return res;
    }
};
```

## Leetcode 57. Insert Interval

* [Leetcode 57. Insert Interval](https://leetcode.com/problems/insert-interval/)

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

> Example 1:
>
> Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].
>
> Example 2:
>
> Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

Push back to the vector and then use the previous merge function.

```cpp
class Solution {
public:
    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {
        vector<Interval> res;
        intervals.push_back(newInterval);
        sort(intervals.begin(), intervals.end(), [](Interval &i, Interval &j){return i.start<j.start;});
        const int n = intervals.size();
        for (int i=0; i<n; i++) {
            if (i+1<n && intervals[i+1].start<=intervals[i].end) {
                intervals[i+1].end = max(intervals[i].end, intervals[i+1].end);
                intervals[i+1].start = min(intervals[i].start, intervals[i+1].start);
            }
            else
                res.push_back(intervals[i]);
        }
        return res;
    }
};
```
