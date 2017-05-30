---
layout:     post
title:      "Leetcode (500) String Series III"
category:   Leetcode
tags:		Leetcode
---

* content
{:toc}

Leetcode String Series III

## Leetcode 500. Keyboard Row

* [Leetcode 500. Keyboard Row](https://leetcode.com/problems/keyboard-row/#/description)

Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.

![](/images/keyboard.png)

Example 1:

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```

```python
class Solution(object):
    def findWords(self, words):
        """
        :type words: List[str]
        :rtype: List[str]
        """
        return [word for row in [set('qwertyuiop'), set('asdfghjkl'), set('zxcvbnm')] for word in words if set(word.lower()) <= row]
```