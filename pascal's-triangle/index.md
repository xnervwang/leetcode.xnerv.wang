# 【LeetCode with Python】 118. Pascal's Triangle
tags: Easy Problems, Array

## 题目
原题页面：<https://leetcode.com/problems/pascals-triangle/><br/>
本文地址：<http://leetcode.xnerv.wang/pascals-triangle/><br/>
题目类型：Array<br/>
难度评价：Easy<br/>
类似题目：[(E) Pascal's Triangle II](/pascals-triangle-ii/)<br/>

> Given *numRows*, generate the first *numRows* of Pascal's triangle.<br/>
><br/>
> For example, given *numRows* = 5,<br/>
> Return<br/>
><br/>
>     [<br/>
>          [1],<br/>
>         [1,1],<br/>
>        [1,2,1],<br/>
>       [1,3,3,1],<br/>
>      [1,4,6,4,1]<br/>
>     ]<br/>

<!-- more -->

---
## 分析
输出帕斯卡三角，明白帕斯卡三角的定义即可简单解题。<br/>

---
## 代码
``` python
class Solution:
    # @return a list of lists of integers
    def generate(self, numRows):
        rows = []
        if numRows <= 0:
            return rows
        if numRows >= 1:
            rows.append([1])
        if numRows >= 2:
            rows.append([1, 1])
        if numRows >= 3:
            need_rowsnum = numRows - 2
            last_row = [1, 1]
            for i in range(0, need_rowsnum):
                new_row = [1]
                for j in range(1, len(last_row)):
                    new_row.append(last_row[j - 1] + last_row[j])
                new_row.append(1)
                rows.append(new_row)
                last_row = new_row
        return rows
```
