# 【LeetCode with Python】 20. Valid Parentheses
tags: Easy Problems, Stack, String

## 题目
原题页面：<https://leetcode.com/problems/valid-parentheses/><br/>
本文地址：<http://leetcode.xnerv.wang/valid-parentheses/><br/>
题目类型：Stack, String<br/>
难度评价：Easy<br/>
类似题目：[(M) Generate Parentheses](/generate-parentheses/), [(H) Longest Valid Parentheses](/longest-valid-parentheses/)<br/>

> Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.<br/>
><br/>
> The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.<br/>

<!-- more -->

---
## 分析
大家肯定在大学时都做过这道题目吧，不过可能相对简单一点，只涉及小括号的配对，这里需要考虑三种括号，不过还是一样的简单。<br/>
用栈来记录遇到的左括号，每次遇到右括号，就从栈中弹出一个左括号，看是不是与该右括号是匹配的。<br/>

---
## 代码
``` python
class Solution:

    def isMatch(self, l ,r):
        return ("(" == l and ")" == r) or ("[" == l and "]" == r) or ("{" == l and "}" == r)

    # @return a boolean
    def isValid(self, s):
        len_s = len(s)
        if 0 == len(s):
            return True
        arr = [ ]
        for ch in s:
            len_arr = len(arr)
            if 0 == len_arr or not self.isMatch(arr[len_arr - 1], ch):
                arr.append(ch)
            else:
                arr.pop()
        return 0 == len(arr)
```
