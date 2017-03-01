---
layout:     post
title:      Leetcode  (94, 144, 145， 102， 107) Binary Tree Traversal (Preorder, Inorder, Level order)
category:   [Leetcode] 
tags:		[Leetcode, Algorithms, Binary Tree]
---

* [Leetcode 144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

Given a binary tree, return the preorder traversal of its nodes' values.

For example:
	Given binary tree {1,#,2,3},
	return [1,2,3].

{% highlight C++ %}
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        if (!root)  return res;
        helper(root, res);
        return res;
    }
    
    void helper(TreeNode* root, vector<int> &res) {
        if (!root)  return;
        res.push_back(root->val);
        helper(root->left, res);
        helper(root->right, res);
    }
};
{% endhighlight %}

* [Leetcode 94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Given a binary tree, return the inorder traversal of its nodes' values.

For example:
	Given binary tree [1,null,2,3],
	return [1,3,2].

{% highlight C++ %}
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if (!root)  return res;
        helper(root, res);
        return res;
    }
    
    void helper(TreeNode* root, vector<int> &res) {
        if (!root)  return;
        helper(root->left, res);
        res.push_back(root->val);
        helper(root->right, res);
    }
};
{% endhighlight %}

* [Leetcode 145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
,
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
	Given binary tree {1,#,2,3},
	return [3,2,1];

{% highlight C++ %}
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        if (!root)  return res;
        helper(root, res);
        return res;
    }
    
    void helper(TreeNode* root, vector<int> &res) {
        if (!root)  return;
        helper(root->left, res);
        helper(root->right, res);
        res.push_back(root->val);
    }
};
{% endhighlight %}

* [Leetcode 102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
	Given binary tree [3,9,20,null,null,15,7],
	return  [
  		[3],
  		[9,20],
  		[15,7]
	]

{% highlight C++ %}
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root)  return res;
        helper(root, res, 0);
        return res;
    }
    
    void helper(TreeNode* root, vector<vector<int>> &res, int depth) {
        if (!root)  return;
        if (res.size() <depth+1)
            res.push_back(vector<int>());
        res[depth].push_back(root->val);
        helper(root->left, res, depth+1);
        helper(root->right, res, depth+1);
    }
};
{% endhighlight %}

* [Leetcode 107. Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
	Given binary tree [3,9,20,null,null,15,7],
	return 
	[
  		[15,7],
  		[9,20],
  		[3]
	]

{% highlight C++ %}
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> res;
        if (!root)  return res;
        helper(root, res, 0);
        reverse(res.begin(), res.end());
        return res;
    }
    
    void helper(TreeNode* root, vector<vector<int>> &res, int depth) {
        if (!root)  return;
        if (res.size() <depth+1)
            res.push_back(vector<int>());
        res[depth].push_back(root->val);
        helper(root->left, res, depth+1);
        helper(root->right, res, depth+1);
    }
};
{% endhighlight %}