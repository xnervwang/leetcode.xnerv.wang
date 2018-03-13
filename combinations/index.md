# 【LeetCode with Python】 77. Combinations
tags: Medium Problems, Backtracking

## 题目
原题页面：<https://leetcode.com/problems/combinations/><br/>
本文地址：<<leetcode-with-python-domain>/combinations/><br/>
题目类型：Backtracking<br/>
难度评价：Medium<br/>
类似题目：[(M) Combination Sum](/combination-sum/), [(M) Permutations](/permutations/)<br/>

> Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.<br/>
><br/>
> For example,<br/>
> If *n* = 4 and *k* = 2, a solution is:<br/>
><br/>
> ```
> [
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
> ]
> ```

<!-- more -->

---
## 分析
一道普通的递归回溯的问题。**这类问题要考虑两个因素：一是做出分支的依据因素，一是结束递归的条件。**<br/>
在这道题目中，做出分支的依据是：是否选择当前的元素。结束递归的条件是：已选择了k个元素，或虽然不足k个元素但已经遍历完全部元素。后面这一个条件尤其要注意，如果忘了加上的话，往往会导致无穷递归（类似于死循环）。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.lists = [ ]

    def doCombine(self, list, n, m, k):
        if 0 == k:
            self.lists.append(list)
            return
        if m > n:
            return
        self.doCombine(list[:], n, m + 1, k)
        new_list = list
        new_list.append(m)
        self.doCombine(new_list, n, m + 1, k - 1)

    # @return a list of lists of integers
    def combine(self, n, k):
        if k > n:
            return [ ]
        self.doCombine([ ], n, 1, k)
        return self.lists
```
