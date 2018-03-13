# 【LeetCode with Python】 52. N-Queens II
tags: Hard Problems, Backtracking

## 题目
原题页面：<https://oj.leetcode.com/problems/n-queens-ii/><br/>
本文地址：<<leetcode-with-python-domain>/n-queens-ii/><br/>
题目类型：Backtracking<br/>
难度评价：Hard<br/>
类似题目：[(H) N-Queens](/n-queens/)<br/>

> Follow up for N-Queens problem.<br/>
><br/>
> Now, instead outputting board configurations, return the total number of distinct solutions.<br/>
><br/>
> ![8-queens](http://www.leetcode.com/wp-content/uploads/2012/03/8-queens.png)<br/>

<!-- more -->

---
## 分析

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.paths_count = 0

    def dpTotalNQueens(self, n, prefix, level):
        for i in range(0, n):
            point = (i, level)
            is_valid = True
            for m in range(0, len(prefix)):
                if i == prefix[m]:
                    is_valid = False
                    break
                if level - m == i - prefix[m] or level - m == prefix[m] - i:
                    is_valid = False
                    break
            if is_valid:
                new_prefix = prefix[:]
                new_prefix.append(i)
                if n - 1 != level:
                    self.dpTotalNQueens(n, new_prefix, level + 1)
                else:
                    self.paths_count += 1

    # @return an integer
    def totalNQueens(self, n):
        self.dpTotalNQueens(n, [ ], 0)
        return self.paths_count
```
