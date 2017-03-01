---
layout:     post
title:      Leetcode  (217, 219, 220) Contains Duplicate I, II, III
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Hash]
---

* [Leetcode 217. Contains Duplicate](https://leetcode.com/problems/merge-two-sorted-lists/)

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

The idea: set doesn't allow the number duplicate input
{% highlight C++ %}
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        return nums.size() > unordered_set<int>(nums.begin(), nums.end()).size();
    }
};
{% endhighlight %}

* [Leetcode 219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)

The idea: use the map to store the nums[i] index
{% highlight C++ %}
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int, int> map;
        for (int i=0; i<nums.size(); i++) {
            if (map[nums[i]]) {
                if (i+1-map[nums[i]] <= k)
                    return true;
            }
            map[nums[i]] = i+1;
        }
        return false;
    }
};
{% endhighlight %}

[Leetcode 220. Contains Duplicate III](https://leetcode.com/problems/contains-duplicate-iii/)

The idea: use the map
{% highlight C++ %}
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        if (nums.empty())   return false;
        map<int, int> m;
        int j = 0;
        for (int i=0; i<nums.size(); i++) {
            if (i-j >k && m[nums[j]]==j)
                m.erase(nums[j++]);
            auto a = m.lower_bound(nums[i]-t);
            if (a!=m.end() && abs(a->first - nums[i])<=t)
                return true;
            m[nums[i]] = i;
        }
        return false;
    }
};
{% endhighlight %}