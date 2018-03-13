# 【LeetCode with Python】 67. Add Binary
tags: Easy Problems, Math, String

## 题目
原题页面：<https://leetcode.com/problems/add-binary/><br/>
本文地址：<<leetcode-with-python-domain>/add-binary/><br/>
题目类型：Math, String<br/>
难度评价：Easy<br/>
类似题目：[(M) Add Two Numbers](/add-two-numbers/), [(M) Multiply Strings](/multiply-strings/), [(E) Plus One](/plus-one/)<br/>

> Given two binary strings, return their sum (also a binary string).<br/>
><br/>
> For example,<br/>
> a = `"11"`<br/>
> b = `"1"`<br/>
> Return `"100"`.<br/>

<!-- more -->

---
## 分析
用字符串模拟二进制整数加法。写了一个更通用的算法，修改self.radix即可将代码改为如八进制整数加法、十进制整数加法等。<br/>
但是在实现过程中，为了处理上的方便，以及为了让代码更简洁，对两个加数的数组做了补零的操作。否则还得分a比b长，b比a长，a和b一样长3种case来处理，代码可能会比较繁琐。<br/>

（由于这里是用Python实现，所以直接用字符串相加这种直观的写法。但实际上从算法效率上考虑，应该实现申请一个size=max(len(a), len(b))+1的字符数组，然后在这个数组中进行模拟加法。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.radix = 2

    # @param a, a string
    # @param b, a string
    # @return a string
    def addBinary(self, a, b):

        a_nums = [(ord(ch) - ord('0')) for ch in a]
        b_nums = [(ord(ch) - ord('0')) for ch in b]
        a_nums_size = len(a_nums)
        b_nums_size = len(b_nums)
        max_nums_size = max(a_nums_size, b_nums_size)
        a_extend_nums = [0 for i in range(0, max_nums_size - a_nums_size)]
        b_extend_nums = [0 for i in range(0, max_nums_size - b_nums_size)]
        a_nums = a_extend_nums + a_nums
        b_nums = b_extend_nums + b_nums
        sum_nums = [0] * max_nums_size

        carry = 0
        for i in range(max_nums_size - 1, -1, -1):
            sum = a_nums[i] + b_nums[i] + carry
            sum_nums[i] = sum % self.radix
            carry = sum / self.radix

        sum_str = ("1" if 1 == carry else "")
        for i in range(0, max_nums_size):
            sum_str += chr(sum_nums[i] + ord('0'))

        return sum_str
```
