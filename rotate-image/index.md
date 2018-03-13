# 【LeetCode with Python】 48. Rotate Image
tags: Medium Problems, Array

## 题目
原题页面：<https://leetcode.com/problems/rotate-image/><br/>
本文地址：<<leetcode-with-python-domain>/rotate-image/><br/>
题目类型：Array<br/>
难度评价：Medium<br/>

> You are given an *n* x *n* 2D matrix representing an image.<br/>
Rotate the image by 90 degrees (clockwise).<br/>
><br/>
> Follow up:<br/>
> Could you do this in-place?<br/>

<!-- more -->

---
## 分析
顺时针90度转动一个二维矩阵，要求in-place的算法，也就不是不能另外开一个新的矩阵然后把原矩阵上的元素一个个对应复制过来，而要在原矩阵上进行操作。<br/>
目前能想到的有两种方法。<br/>

1. 第一种比较直观，首先将原矩阵按照水平轴上下翻转，然后按照左上到右下的对角线再反转，则等价于90度顺时针转动。这个方法的缺点是要反转两次，优点是直观，不容易出错。<br/>
2. 第二种方法每个元素只需要调整一次，但是转化公式会比较复杂。对于矩阵matrix[n][n]中的某一点matrix[x][y]（0<=x, y&lt;n），90度顺时针转动后到了matrix[y][n-x-1]，而matrix[y][n-x-1]到了matrix[n-x-1][n-y-1]，matrix[n-x-1][n-y-1]到了matrix[n-y-1][x]，matrix[n-y-1][x]又到了matrix[x][y]，可见这四个点正好实现了一次旋转互换。<br/>

本文采用第二种方法，空间复杂度O(1)，时间复杂度O(n*n)。<br/>

---
## 代码
``` python
class Solution:
    # @param matrix, a list of lists of integers
    # @return nothing (void), do not return anything, modify matrix in-place instead.
    def rotate(self, matrix):
        n = len(matrix)
        if 1 == n:
            return
        round = int(n / 2)
        for x in range(0, round):
            for y in range(x, n - x - 1):
                matrix[n - y - 1][x], matrix[n - x - 1][n - y - 1], matrix[y][n - x - 1], matrix[x][y] = matrix[n - x - 1][n - y - 1], matrix[y][n - x - 1], matrix[x][y], matrix[n - y - 1][x]
```
