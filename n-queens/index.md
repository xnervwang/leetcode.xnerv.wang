# 【LeetCode with Python】 51. N-Queens
tags: Hard Problems, Backtracking

## 题目
原题页面：<https://oj.leetcode.com/problems/n-queens/><br/>
本文地址：<<leetcode-with-python-domain>/n-queens/><br/>
题目类型：Backtracking<br/>
难度评价：Hard<br/>
类似题目：[(H) N-Queens II](/n-queens-ii/)<br/>

> The *n*-queens puzzle is the problem of placing *n* queens on an *n*×*n* chessboard such that no two queens attack each other.<br/>
><br/>
> ![8-queens](http://www.leetcode.com/wp-content/uploads/2012/03/8-queens.png)<br/>
><br/>
> Given an integer *n*, return all distinct solutions to the *n*-queens puzzle.<br/>
><br/>
> Each solution contains a distinct board configuration of the *n*-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.<br/>
><br/>
> For example,<br/>
> There exist two distinct solutions to the 4-queens puzzle:<br/>
>> `<br/>
[<br/>
[".Q..",  // Solution 1<br/>
"...Q",<br/>
"Q...",<br/>
"..Q."],`<br/>
>> `<br/>
["..Q.",  // Solution 2<br/>
"Q...",<br/>
"...Q",<br/>
".Q.."]<br/>
]`<br/>

<!-- more -->

---
## 分析
下标计算处理，控制好循环条件，下标不要越界即可。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.paths = [ ]

    def dpSolveNQueens(self, n, prefix, level):
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
                    self.dpSolveNQueens(n, new_prefix, level + 1)
                else:
                    self.paths.append(new_prefix)

    # @return a list of lists of string
    def solveNQueens(self, n):
        self.dpSolveNQueens(n, [ ], 0)
        lists = [ ]
        for path in self.paths:
            list = [ ]
            for num in path:
                str = "." * num + "Q" + "." * (n - num - 1)
                list.append(str)
            lists.append(list)
        return lists
```
