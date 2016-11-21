---
layout:     post
title:      Leetcode  (20, 22, 32, 241) Parentheses Series
category:   [Leetcode] 
tags:		[Leetcode, algorithms, recursion]
---

* [Leetcode 20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
{% highlight C++ %}
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        if (s.empty())  return true;
        for (int i=0; i<s.size(); i++) {
            char sign = s[i];
            if (s[i]=='[' || s[i]=='(' || s[i]=='{')
                st.push(sign);
            else {
                if (st.empty()) return false;
                if (sign==')') {
                    if (st.top() != '(')    return false;
                    else    st.pop();
                }
                else if (sign==']') {
                    if (st.top() != '[')    return false;
                    else    st.pop();
                }
                else {
                    if (st.top() != '{')    return false;
                    else    st.pop();
                }
            }
        }
        return st.size()==0;
    }
};
{% endhighlight %}

* [Leetcode 22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]

{% highlight C++ %}
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        if (n<=0)   return res;
        string str;
        helper(res, str, 0, n);
        return res;
    }
    void helper(vector<string> &res, string str, int right, int left) {
        if (left==0 && right==0) {
            res.push_back(str);
            return;
        }
        
        if (right>0)
            helper(res, str+")", right-1, left);
        if (left>0)
            helper(res, str+"(", right+1, left-1);
    }
};
{% endhighlight %}

* [Leetcode 32. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

For "(()", the longest valid parentheses substring is "()", which has length = 2.

Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

{% highlight C++ %}
class Solution {
public:
    int longestValidParentheses(string input) {
        if (input.empty())  return 0;
        stack<int> st;
        int last = -1;
        int res = 0;
        for (int i=0; i<input.size(); i++) {
            if (input[i]=='(')  st.push(i);
            else {
                if (st.empty()) last = i;
                else {
                    st.pop();
                    if (st.empty()) res = max(res, i-last);
                    else    res = max(res, i-st.top());
                }
            }
        }
        return res;
    }
};
{% endhighlight %}

* [Leetcode 241. Different Ways to Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/)

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.


Example 1

Input: "2-1-1".

	((2-1)-1) = 0
	(2-(1-1)) = 2
	Output: [0, 2]

Example 2

Input: "2*3-4*5"

	(2*(3-(4*5))) = -34
	((2*3)-(4*5)) = -14
	((2*(3-4))*5) = -10
	(2*((3-4)*5)) = -10
	(((2*3)-4)*5) = 10
	Output: [-34, -14, -10, -10, 10]

{% highlight C++ %}
class Solution {
public:
    vector<int> diffWaysToCompute(string input) {
        vector<int> res;
        if (input.empty())  return res;
        const int n = input.size();
        for (int i=0; i<n; i++) {
            char sign = input[i];
            if (sign =='+' || sign=='-' || sign =='*') {
                vector<int> temp1 = diffWaysToCompute(input.substr(0, i));
                vector<int> temp2 = diffWaysToCompute(input.substr(i+1));
                for (int num1:temp1) {
                    for (int num2:temp2) {
                        if (sign=='+')  res.push_back(num1+num2);
                        else if (sign=='-') res.push_back(num1-num2);
                        else    res.push_back(num1*num2);
                    }
                }
            }
        }
        if (res.empty())
            res.push_back(stoi(input));
        return res;
    }
};
{% endhighlight %}