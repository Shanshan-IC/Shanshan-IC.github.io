---
layout:     post
title:      "Leetcode  (36, 37) Sudoku"
category:   Leetcode
tags:		Leetcode Math
---

* content
{:toc}

## Leetcode 36. Valid Sudoku

* [Leetcode 36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/#/description)

Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

![](/images/sudoku.png)

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        if (board.empty())  return false;
        const int n = board.size();
        vector<int> count;
        // row
        for (int i=0; i<n; i++) {
            count.assign(9, 0);
            for (int j=0; j<n; j++) {
                if (board[i][j]!='.') {
                    int pos = board[i][j]-'1';
                    if (count[pos]>0)   return false;
                    else    ++count[pos];
                }
            }
        }
        //column
        for (int j=0; j<n; j++) {
            count.assign(9, 0);
            for (int i=0; i<n; i++) {
                if (board[i][j]!='.') {
                    int pos = board[i][j]-'1';
                    if (count[pos]>0)   return false;
                    else    ++count[pos];
                }
            }
        }
        //3*3 chunk
        for (int i=0; i<n; i+=3) {
            for (int j=0; j<n; j+=3) {
                count.assign(9, 0); 
                for (int row=i; row<i+3; row++) 
                    for (int col=j; col<j+3; col++) {
                        if (board[row][col]!='.') {
                            int pos = board[row][col]-'1';
                            if (count[pos]>0)   return false;
                            else    ++count[pos];
                        }
                    }
            }
        }
        return true;
    }
};
```

## Leetcode 37. Sudoku Solver

* [Leetcode 37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/#/description)

Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.

```cpp
class Solution {
public:
    bool solveSudoku(vector<vector<char>>& board) {
        for (int i = 0; i < 9; ++i)
            for (int j = 0; j < 9; ++j) 
                if (board[i][j] == '.') {
                    for (int k = 0; k < 9; ++k) {
                        board[i][j] = '1' + k;
                        if (isValid(board, i, j) && solveSudoku(board))
                            return true;
                        board[i][j] = '.';
                    }
                    return false;
                }
        return true;
    }
    
    bool isValid(const vector<vector<char> > &board, int x, int y) {
        int i, j;
        for (i = 0; i < 9; i++) 
            if (i != x && board[i][y] == board[x][y])
                return false;
        for (j = 0; j < 9; j++) 
            if (j != y && board[x][j] == board[x][y])
                return false;
        for (i = 3 * (x / 3); i < 3 * (x / 3 + 1); i++)
            for (j = 3 * (y / 3); j < 3 * (y / 3 + 1); j++)
                if ((i != x || j != y) && board[i][j] == board[x][y])
                    return false;
        return true;
    }

};
```