---
layout:     post
title:      Leetcode  (100, 101, 104, 226) Binary Tree Series
category:   [Leetcode] 
tags:		[Leetcode, algorithms, binary tree, recursion]
---

{% highlight C++ %}
struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
{% endhighlight %}

* [Leetcode 101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

{% highlight C++ %}
class Solution {
public:
    bool isEqual(TreeNode* p, TreeNode* q) {
        if (!p && !q)   return true;
        if (!p || !q ||p->val != q->val)    return false;
        return isEqual(p->left, q->right) && isEqual(p->right, q->left);
    }
    
    bool isSymmetric(TreeNode* root) {
        if (!root)  return true;
        return isEqual(root->left, root->right);
    }
};
{% endhighlight %}

* [Leetcode 226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

Invert a binary tree.
{% highlight C++ %}
class Solution {
public:
    TreeNode* invertTree(TreeNode* tree) {
        if (!tree)  return tree;
        TreeNode* temp = tree->left;
        tree->left = invertTree(tree->right);
        tree->right = invertTree(temp);
        return tree;
    }
};
{% endhighlight %}

* [Leetcode 100. Same Tree](https://leetcode.com/problems/same-tree/)

Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

{% highlight C++ %}
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (!root)  return 0;
        return max(1+maxDepth(root->left), 1+maxDepth(root->right));
    }
};
{% endhighlight %}

* [Leetcode 104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
{% highlight C++ %}
class Solution {
public:
    bool isSameTree(TreeNode* tree1, TreeNode* tree2) {
        if (!tree1 && !tree2)   return true;
        if (!tree1 || !tree2 || tree1->val != tree2->val)    return false;
        return isSameTree(tree1->left, tree2->left) && isSameTree(tree1->right, tree2->right);
    }
};
{% endhighlight %}

