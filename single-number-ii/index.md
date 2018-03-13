# 【LeetCode with Python】 137. Single Number II
tags: Medium Problems, Bit Manipulation

## 题目
原题页面：<https://oj.leetcode.com/problems/single-number-ii/><br/>
本文地址：<<leetcode-with-python-domain>/single-number-ii/><br/>
题目类型：Bit Manipulation<br/>
难度评价：Medium<br/>
类似题目：[(M) Single Number](/single-number/), [(M) Single Number III](/single-number-III/)<br/>

> Given an array of integers, every element appears *three* times except for one. Find that single one.<br/>
><br/>
> **Note:**<br/>
> Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?<br/>

<!-- more -->

---
## 分析
与Single Number相比，前者是每个元素出现两次（除了一个特殊元素），而本题是每个元素出现三次（除了一个特殊元素）。<br/>
int数据共有32位，可以用32变量存储这N个元素中各个二进制位上1出现的次数，最后在进行模三操作，如果为1，那说明这一位是要找元素二进制表示中为1的那一位。但是这种做法估计不是最好的，应该有更好的算法，思考中。<br/>

---
## 代码
``` python
class Solution:
    # @param A, a list of integer
    # @return an integer
    def singleNumber(self, A):
        len_A = len(A)
        counts = [0] * 32
        res = 0
        for i in range(0, 32):
            for num in A:
                #num = long(num)     # it will make time limit exceeded
                counts[i] += (num>>i) & 1
            res |= ((counts[i] % 3) << i)
        if 0 != counts[31] % 3:
            res -= pow(2, 32)         ######
        return res
```
