---
layout:     post
title:      Leetcode  (108, 109) Convert Sorted Array/List to Binary Search Tree
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Binary Search Tree]
---

*[Leetcode 108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

{% highlight C++ %}
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return helper(nums, 0, nums.size()-1);
    }
    
    TreeNode* helper(vector<int> &nums, int i, int j) {
        if (i>j)    return NULL;
        int mid = i+(j-i)/2;
        TreeNode* node = new TreeNode(nums[mid]);
        node->left = helper(nums, i, mid-1);
        node->right = helper(nums, mid+1, j);
        return node;
    }
};
{% endhighlight %}

*[Leetcode 109. Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

{% highlight C++ %}
class Solution {
public:
    TreeNode* sortedListToBST(ListNode* head) {
        if (!head)  return NULL;
        if (!head->next)    return new TreeNode(head->val);
        
        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* tail = NULL;
        while (fast && fast->next) {
            tail = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        tail->next = NULL;
        TreeNode* node = new TreeNode(slow->val);
        node->left = sortedListToBST(head);
        node->right = sortedListToBST(slow->next);
        return node;
    }
};
{% endhighlight %}
