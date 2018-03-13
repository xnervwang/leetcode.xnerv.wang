# 【LeetCode with Python】 59. Spiral Matrix II
tags: Medium Problems, Array

## 题目
原题页面：<https://oj.leetcode.com/problems/spiral-matrix-ii/><br/>
本文地址：<<leetcode-with-python-domain>/spiral-matrix-ii/><br/>
题目类型：Array<br/>
难度评价：Medium<br/>
类似题目：[(M) Spiral Matrix](/spiral-matrix/)<br/>

> Given an integer *n*, generate a square matrix filled with elements from 1 to *n*<sup>2</sup> in spiral order.<br/>
><br/>
> For example,<br/>
> Given *n* = `3`,<br/>
><br/>
> You should return the following matrix:<br/>
> `<br/>
[<br/>
[ 1, 2, 3 ],<br/>
[ 8, 9, 4 ],<br/>
[ 7, 6, 5 ]<br/>
]<br/>
> `<br/>

<!-- more -->

---
## 分析
跟[(M) Spiral Matrix](/spiral-matrix/)类似，使用两重for循环，但不是输出螺旋状遍历的元素，而是螺旋状地将元素填入到二维数组中。<br/>

---
## 代码
``` python
class Solution:
    # @return a list of lists of integer
    def generateMatrix(self, n):

        if 0 == n:
            return [ ]
        m = n
        index = 1
        matrix = [[0 for x in range(0, n)] for y in range(0, n)]
        round = (n + 1) / 2
        for x in range(0, round):
            for y in range(x, n - x):
                matrix[x][y] = index
                index += 1
            for y in range(x + 1, m - x - 1):
                matrix[y][n - x - 1] = index
                index += 1
            if m - 2 * x > 1:  ###
                for y in range(n - x - 1, x - 1, -1):
                    matrix[m - x - 1][y] = index
                    index += 1
            if n - 2 * x > 1:      ###
                for y in range(m - x - 2, x, -1):   ###
                    matrix[y][x] = index
                    index += 1
        return matrix
```
