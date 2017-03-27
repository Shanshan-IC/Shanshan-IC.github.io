---
layout:     post
title:      "Leetcode (77, 79) DFS Series"
category:   Leetcode
tags:		Leetcode DFS
---

* content
{:toc}

Leetcode DFS Series

## Leetcode 77. Combinations

* [Leetcode 77. Combinations](https://leetcode.com/problems/combinations/#/description)

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

`
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
`

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> curr;
        if (n<k)    return res;
        helper(res, curr, 1, n, k);
        return res;
    }
    
    void helper(vector<vector<int>> &res, vector<int> &curr, int pos, int n, int k) {
        if (k==0){
            res.push_back(curr);
            return;
        }
        for (int i=pos; i<=n; i++) {
            curr.push_back(i);
            helper(res, curr, i+1, n, k-1);
            curr.pop_back();
        }
    }
};
```

## Leetcode 79. Word Search

* [Leetcode 79. Word Search](https://leetcode.com/problems/word-search/#/description)

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given board =

`
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
`

word = "ABCCED", -> returns `true`,

word = "SEE", -> returns `true`,

word = "ABCB", -> returns `false`.

```cpp
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if (board.empty() || word.empty())  return false;
        const int m = board.size();
        const int n = board[0].size();
        for (int i=0; i<m; i++)
            for (int j=0; j<n; j++)
                if (board[i][j]==word[0])
                    if (helper(board, word, i, j, 0, m, n))
                        return true;
        return false;
    }
    
    bool helper(vector<vector<char>> &board, string word, int i, int j, int pos, int m, int n) {
        if (pos==word.size())   return true;
        if (i<0 || j<0 || i>=m || j>=n || board[i][j]=='@' || board[i][j]!=word[pos])
            return false;
        char temp = board[i][j];
        board[i][j] = '@';
        if (helper(board, word, i-1, j, pos+1, m, n) || helper(board, word, i+1, j, pos+1, m, n) || helper(board, word, i, j-1, pos+1, m, n) | helper(board, word, i, j+1, pos+1, m, n))
            return true;
        board[i][j] = temp;
        return false;
    }
};
```