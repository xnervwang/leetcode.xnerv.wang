# 【LeetCode with Python】 54. Spiral Matrix
tags: Medium Problems, Array

## 题目
原题页面：<https://oj.leetcode.com/problems/spiral-matrix/><br/>
本文地址：<<leetcode-with-python-domain>/spiral-matrix/><br/>
题目类型：Array<br/>
难度评价：Medium<br/>
类似题目：[(M) Spiral Matrix II](/spiral-matrix-II/)<br/>

> Given a matrix of `m` x `n` elements (`m` rows, `n` columns), return all elements of the matrix in spiral order.<br/>
><br/>
> For example,<br/>
> Given the following matrix:<br/>
> `[<br/>
[ 1, 2, 3 ],<br/>
[ 4, 5, 6 ],<br/>
[ 7, 8, 9 ]<br/>
]`<br/>
> You should return `[1,2,3,6,9,8,7,4,5]`.<br/>

<!-- more -->

---
## 分析
还是一道下标计算的题目，用两重嵌套for循环，以螺旋状的方式遍历二维数组。<br/>

---
## 代码
``` python
class Solution:
    # @param matrix, a list of lists of integers
    # @return a list of integers
    def spiralOrder(self, matrix):

        m = len(matrix)
        if 0 == m:
            return [ ]
        n = len(matrix[0])
        if 0 == n:
            return [ ]
        arr = [ ]

        round = (min(m, n) + 1) / 2
        for x in range(0, round):
            for y in range(x, n - x):
                arr.append(matrix[x][y])
            for y in range(x + 1, m - x - 1):
                arr.append(matrix[y][n - x - 1])
            if m - 2 * x > 1:  ###
                for y in range(n - x - 1, x - 1, -1):
                    arr.append(matrix[m - x - 1][y])
            if n - 2 * x > 1:      ###
                for y in range(m - x - 2, x, -1):   ###
                    arr.append(matrix[y][x])
        return arr
```
