# 【LeetCode with Python】 136. Single Number
tags: Medium Problems, Hash Table, Bit Manipulation

## 题目
原题页面：<https://leetcode.com/problems/single-number/><br/>
本文地址：<<leetcode-with-python-domain>/single-number/><br/>
题目类型：Medium<br/>
难度评价：Hash Table, Bit Manipulation<br/>
类似题目：[(M) Single Number II](/single-number-ii/), [(M) Single Number III](/single-number-iii/), [(M) Missing Number](/missing-number/), [(H) Find the Duplicate Number](/find-the-duplicate-number/)<br/>

> Given an array of integers, every element appears *twice* except for one. Find that single one.<br/>
><br/>
> **Note:**<br/>
> Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?<br/>

<!-- more -->

---
## 分析
编程之美上好像也出现过类似的题目。关键是异或操作（异或支持交换律），知道的人立马能做出来，不知道的人想破脑袋也想不出这个方法。当然用hashmap/map之类的把所有元素插一遍也能找出这个只出现过一次的元素，但是想必面试官不会很开心。位操作还是有很多技巧的，还需要继续深入学习。<br/>
此外还可以参考[Single Number II](/single-number-ii/)。<br/>

---
## 代码
``` python
class Solution:
    # @param A, a list of integer
    # @return an integer
    def singleNumber(self, A):
        len_A = len(A)
        if 0 == len_A:
            return 0
        elif 1 == len_A:
            return A[0]
        else:
            result = A[0]
            for i in range(1, len_A):
                result ^= A[i]
        return result
```
