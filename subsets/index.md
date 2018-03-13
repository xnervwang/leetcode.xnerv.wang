# 【LeetCode with Python】 78. Subsets
tags: Medium Problems, Array, Backtracking, Bit Manipulation

## 题目
原题页面：<https://leetcode.com/problems/subsets/><br/>
本文地址：<http://leetcode.xnerv.wang/subsets/><br/>
题目类型：Array, Backtracking, Bit Manipulation<br/>
难度评价：Medium<br/>

> Given a set of distinct integers, <i>nums</i>, return all possible subsets.<br/>
><br/>
> **Note:**<br/>
><br/>
> * Elements in a subset must be in non-descending order.<br/>
> * The solution set must not contain duplicate subsets.<br/>
><br/>
> For example,<br/>
> If ***nums*** = `[1,2,3]`, a solution is:<br/>
><br/>
>     [<br/>
>       [3],<br/>
>       [1],<br/>
>       [2],<br/>
>       [1,2,3],<br/>
>       [1,3],<br/>
>       [2,3],<br/>
>       [1,2],<br/>
>       []<br/>
>     ]<br/>

<!-- more -->

---
## 分析
普通的搜索算法即可解决，不过注意每个子序列都要以升序排列，所以从一开始就把输入的S排好序，一了百了，不知道是否还有其它更好的算法。<br/>
递归回溯的两个关键：递和归。递即分支条件，在本题里指的是是否选择某个元素，而形成每次的两个分支。归即结束条件，在本题里指已经考察完全部元素。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.results = [ ]

    def doSubsets(self, S, cur_list, cur_index):
        if cur_index > len(S) - 1:
            self.results.append(cur_list)
            return
        cur_list0 = cur_list[:]
        cur_list1 = cur_list[:]
        cur_list1.append(S[cur_index])
        self.doSubsets(S, cur_list0, cur_index + 1)
        self.doSubsets(S, cur_list1, cur_index + 1)

    # @param S, a list of integer
    # @return a list of lists of integer
    def subsets(self, S):
        S.sort()
        self.doSubsets(S, [ ], 0)
        return self.results
```
