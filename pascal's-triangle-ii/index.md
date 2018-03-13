# 【LeetCode with Python】 119. Pascal's Triangle II
tags: Easy Problems, Array

## 题目
原题页面：<https://leetcode.com/problems/pascals-triangle-ii/><br/>
本文地址：<<leetcode-with-python-domain>/pascals-triangle-ii/><br/>
题目类型：Array<br/>
难度评价：Easy<br/>
类似题目：[(E) Pascal's Triangle](/pascals-triangle/)<br/>

> Given an index *k*, return the *k*<sup>th</sup> row of the Pascal's triangle.<br/>
><br/>
> For example, given *k* = 3,<br/>
> Return `[1,3,3,1]`.<br/>
><br/>
> **Note:**<br/>
> Could you optimize your algorithm to use only *O*(*k*) extra space?<br/>

<!-- more -->

---
## 分析
和Pascal's Triangle类似的题目，不过要求的不是输出整个帕斯卡三角，而是输出其中的某一层了。<br/>

---
## 代码
``` python
class Solution:
    # @return a list of lists of integers
    def getRow(self, rowIndex):
        if rowIndex <= 0:
            return [1]
        elif 1 == rowIndex:
            return [1, 1]
        elif rowIndex >= 2:
            need_rowsnum = rowIndex - 1
            last_row = [1, 1]
            for i in range(0, need_rowsnum):
                new_row = [1]
                for j in range(1, len(last_row)):
                    new_row.append(last_row[j - 1] + last_row[j])
                new_row.append(1)
                last_row = new_row
            return last_row
```
