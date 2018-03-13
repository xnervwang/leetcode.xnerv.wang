# 【LeetCode with Python】 90. Subsets II
tags: Medium Problems, Array, Backtracking

## 题目
原题页面：<https://leetcode.com/problems/subsets-ii/><br/>
本文地址：<http://leetcode.xnerv.wang/subsets-ii/><br/>
题目类型：Array, Backtracking<br/>
难度评价：Medium<br/>

> Given a collection of integers that might contain duplicates,***nums***, return all possible subsets.<br/>
><br/>
> **Note:**<br/>
><br/>
> * Elements in a subset must be in non-descending order.<br/>
> * The solution set must not contain duplicate subsets.<br/>
><br/>
> For example,<br/>
> If ***nums*** = `[1,2,2]`, a solution is:<br/>
><br/>
>     [<br/>
>       [2],<br/>
>       [1],<br/>
>       [1,2,2],<br/>
>       [2,2],<br/>
>       [1,2],<br/>
>       []<br/>
>     ]<br/>

<!-- more -->

---
## 分析
与Subsets差不多，先对输入的列表S排序，唯一需要改动的是只是需要在每次递归的时候记忆前一个字符，从而避免一种情况：相等的字符，如果前一个没有才采纳，则后面的字符则也不能被采纳，通过这种方式可以避免产生重复的子序列。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.results = [ ]

    def doSubsets(self, S, cur_list, cur_index, last_ch, add_last_ch):
        if cur_index > len(S) - 1:
            self.results.append(cur_list)
            return
        cur_list0 = cur_list[:]
        self.doSubsets(S, cur_list0, cur_index + 1, S[cur_index], False)
        if not last_ch == S[cur_index] or add_last_ch:
            cur_list1 = cur_list[:]
            cur_list1.append(S[cur_index])
            self.doSubsets(S, cur_list1, cur_index + 1, S[cur_index], True)

    # @param num, a list of integer
    # @return a list of lists of integer
    def subsetsWithDup(self, S):
        S.sort()
        self.doSubsets(S, [ ], 0, "", False)
        return self.results
```
