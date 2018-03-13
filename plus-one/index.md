# 【LeetCode with Python】 66. Plus One
tags: Easy Problems, Array, Math

## 题目
原题页面：<https://leetcode.com/problems/plus-one/><br/>
本文地址：<<leetcode-with-python-domain>/plus-one/><br/>
题目类型：Array, Math<br/>
难度评价：Easy<br/>
类似题目：[(M) Multiply Strings](/multiply-strings/), [(E) Add Binary](/add-binary/)<br/>

> Given a non-negative number represented as an array of digits, plus one to the number.<br/>
><br/>
> The digits are stored such that the most significant digit is at the head of the list.<br/>

<!-- more -->

---
## 分析
用一个int数组代表一个数值，最左边是最高位，现要求加上1，同样地返回一个int数组代表计算结果。<br/>
非常简单的模拟加法，注意进位问题，如果是99，999这种，最后加上1后还要在数组最左边插入一个元素1。<br/>
无论最高位有没有发生进位，空间复杂度都是O(1)。时间复杂度是O(N)。<br/>

---
## 代码
``` python
class Solution:
    # @param digits, a list of integer digits
    # @return a list of integer digits
    def plusOne(self, digits):
        len_s = len(digits)
        carry = 1
        for i in range(len_s - 1, -1, -1):
            total = digits[i] + carry
            digit = int(total % 10)
            carry = int(total / 10)
            digits[i] = digit
        if 1 == carry:
            digits.insert(0, 1)
        return digits
```
