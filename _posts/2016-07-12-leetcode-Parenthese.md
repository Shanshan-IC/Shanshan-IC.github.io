---
layout:     post
title:      Leetcode  (20, 241) Parentheses Series
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