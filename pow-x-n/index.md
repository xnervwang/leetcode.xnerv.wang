# 【LeetCode with Python】 50. Pow(x, n)
tags: Medium Problems, Math, Binary Search

## 题目
原题页面：<https://leetcode.com/problems/powx-n/><br/>
本文地址：<http://leetcode.xnerv.wang/powx-n/><br/>
题目类型：Math, Binary Search<br/>
难度评价：Medium<br/>
类似题目：[(M) Sqrt(x)](/sqrtx/)<br/>

Implement pow(*x*, *n*).<br/>

<!-- more -->

---
## 分析
用n个x相乘显然不是应该出现在leetcode上的算法。这里是利用二分的算法，通过递归来加速计算。<br/>
例如，pow(x, 5) == (x * pow(x, 4)) == (x * pow(pow(x, 2), 2))。<br/>

---
## 代码
``` python
class Solution:
    # @param x, a float
    # @param n, a integer
    # @return a float
    def pow(self, x, n):
        if 0 == n:
            return 1
        elif n < 0:
            return 1.0 / self.pow(x, -n)
        else:
            half = self.pow(x, n >> 1)
            if 0 == n % 2:
                return half * half
            else:
                return x * half * half
```
