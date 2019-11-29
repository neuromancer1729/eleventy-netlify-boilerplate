---
title: Interview Questions
date: 2019-11-29T05:23:08.757Z
summary: List of interview questions
tags:
  - post
---
Q.) Without using library functions implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

A.) The ASCII codes for A-Z is 65-90 and those for a-z is that range plus 32.

```
    def toLowerCase(self, str):
        res =""
        for char in str:
            if ord(char) >=65 and ord(char) <= 90:
                res +=chr(ord(char)+32)
            else:
                res+=char
        
        return res
        
```

Q.)Given a string containing just the characters '(', ')', '{', '}', '\[' and ']', determine if the input string is valid. <https://leetcode.com/problems/valid-parentheses/>

A.) 

```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if len(s) ==0: return True
        for i in range(len(s)):
            if s[i:i+2] in ['()','{}','[]']:
                p = s[:i] + s[i+2:]
                if len(p) ==0:
                    return True
                return self.isValid(p)
        return False
                
```

This solution has O(n square) complexity. Here is a more optimal solution

```
class Solution(object):
    def isValid(self, s):
        stack = []

        mapping = {")": "(", "}": "{", "]": "["}

        for char in s:
            if char in mapping:
                top_element = stack.pop() if stack else '#'
                if mapping[char] != top_element:
                    return False
            else:
                stack.append(char)

        return not stack
```
