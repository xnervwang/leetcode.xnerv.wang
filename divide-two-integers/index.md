# 【LeetCode with Python】 29. Divide Two Integers
tags: Medium Problems, Math, Binary Search

## 题目
原题页面：<https://leetcode.com/problems/divide-two-integers/><br/>
本文地址：<<leetcode-with-python-domain>/divide-two-integers/><br/>
题目类型：Math, Binary Search<br/>
难度评价：Medium<br/>

> Divide two integers without using multiplication, division and mod operator.<br/>
><br/>
> If it is overflow, return MAX_INT.<br/>

<!-- more -->

---
## 分析

---
## 代码
``` python
class Solution:
    # @return an integer
    def divide(self, dividend, divisor):

        if 0 == divisor or 0 == dividend:
            return 0
        elif 1 == divisor or -1 == divisor:
            return dividend * divisor

        positive = 1
        if (dividend >0 and divisor < 0) or (dividend < 0 and divisor > 0):
            positive = -1
        dividend = dividend if dividend > 0 else -dividend
        divisor = divisor if divisor > 0 else -divisor

        result = 0
        dividend_now = dividend
        while dividend_now >= divisor:
            total = divisor
            sub_result = 1
            while True:
                total = total << 1
                sub_result = sub_result << 1   ## not += 2
                if total > dividend_now:
                    total = total >> 1
                    sub_result = sub_result >> 1
                    break
                elif total == dividend_now:
                    break
            result += sub_result
            dividend_now -= total
        return result * positive
```
