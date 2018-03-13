# 【LeetCode with Python】 22. Generate Parentheses
tags: Medium Problems, Backtracking, String

## 题目
原题页面：<https://leetcode.com/problems/generate-parentheses/><br/>
本文地址：<<leetcode-with-python-domain>/generate-parentheses/><br/>
题目类型：Backtracking, String<br/>
难度评价：Medium<br/>

> Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.<br/>
><br/>
> For example, given *n* = 3, a solution set is:<br/>
><br/>
> `"((()))", "(()())", "(())()", "()(())", "()()()"`<br/>

<!-- more -->

---
## 分析
常见的递归回溯题目，要求左右括号匹配出现。只要符合一个规则即可认为是匹配：从左往右遍历时，左括号的数量>=右括号的数量。因此，每一层递归时，有两种分支选择：添加左括号，或者添加右括号。某一个分支能否继续，取决于是否符合上述规则。而判断分支的结束，就在于n个左括号和n个右括号都已经出现完。<br/>
代码中的left_count是记录当前层次递归时已经出现过的左括号数，left_remain是记录可供“消耗”的左括号数，即当前左括号数减去右括号数。Python的两个列表相加，表示将两个子列表合并成一个列表，如[1, 2] + [3] = [1, 2, 3]。<br/>

---
## 代码
``` python
class Solution:

    def doGenerateParenthesis(self, n, left_count, left_remain, prefix):

        # only one out-point: the string has been finished.
        if n == left_count and 0 == left_remain:
            return [ prefix ]

        left_list = [ ]
        right_list = [ ]
        if left_count < n:
            left_list = self.doGenerateParenthesis(n, left_count + 1, left_remain + 1, prefix + "(")
        if left_remain > 0:
            right_list = self.doGenerateParenthesis(n, left_count, left_remain - 1, prefix + ")")

        return left_list + right_list

    # @param an integer
    # @return a list of string
    def generateParenthesis(self, n):
        if 0 == n:
            return [ ]
        else:
            list = self.doGenerateParenthesis(n, 0, 0, "")
            return list
```
