# 【LeetCode with Python】 150. Evaluate Reverse Polish Notation
tags: Medium Problems, Stack

## 题目
原题页面：<https://leetcode.com/problems/evaluate-reverse-polish-notation/><br/>
本文地址：<<leetcode-with-python-domain>/evaluate-reverse-polish-notation/><br/>
题目类型：Stack<br/>
难度评价：Medium<br/>
类似题目：[(M) Basic Calculator](/basic-calculator/), [(H) Expression Add Operators](/expression-add-operators/)<br/>

> Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).<br/>
><br/>
> Valid operators are `+`, `-`, `*`, `/`. Each operand may be an integer or another expression.<br/>
><br/>
> Some examples:<br/>
><br/>
>       ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9<br/>
>       ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6<br/>

<!-- more -->

---
## 分析
逆波兰式（后缀表达式）的计算。相信大多数计算机和软件专业的朋友大学时都做过的算法题，用栈模拟计算过程。<br/>
但是从原题给的examples看来的话，题目要求的除法其实是整除，在Python中就是//，在C/C++中就是int/int。<br/>

---
## 代码
``` python
class Solution:

    # @param tokens, a list of string
    # @return an integer
    def evalRPN(self, tokens):

        len_tokens = len(tokens)
        if 0 == len_tokens:
            return 0

        # python has no stack, so we have to simulate it
        nums_stack = []

        for i in range(0, len_tokens):
            token = tokens[i]
            # consider negative number, so shouldn't decide by the first char, but last char
            last_ch = token[len(token) - 1]
            if last_ch >= '0' and last_ch <= '9':
                nums_stack.append(int(token))
            else:
                right = nums_stack.pop()
                left = nums_stack.pop()
                if '+' == token:
                    result = left + right
                elif '-' == token:
                    result = left - right
                elif '*' == token:
                    result = left * right
                else:
                    sign = 1 if (left >= 0 and right >= 0) or (left <= 0 and right <= 0) else -1
                    result = abs(left) // abs(right) * sign
                nums_stack.append(result)

        return nums_stack.pop()
```
