# 【LeetCode with Python】 40. Combination Sum II
tags: Medium Problems, Array, Backtracking

## 题目
原题页面：<https://leetcode.com/problems/combination-sum-ii/><br/>
本文地址：<<leetcode-with-python-domain>/combination-sum-ii/><br/>
题目类型：Array, Backtracking<br/>
难度评价：Medium<br/>
类似题目：[(M) Combination Sum](/combination-sum/)<br/>

> Given a collection of candidate numbers (***C***) and a target number (***T***), find all unique combinations in ***C*** where the candidate numbers sums to ***T***.<br/>
><br/>
> Each number in ***C*** may only be used **once** in the combination.<br/>
><br/>
> **Note:**<br/>
><br/>
> * All numbers (including target) will be positive integers.<br/>
> * Elements in a combination (*a*<sub>1</sub>, *a*<sub>2</sub>, … , *a*<sub>k</sub>) must be in non-descending order. (ie, *a*<sub>1</sub> ≤ *a*<sub>2</sub> ≤ … ≤ *a*<sub>k</sub>).<br/>
> * The solution set must not contain duplicate combinations.<br/>

> For example, given candidate set `10,1,2,7,6,1,5` and target `8`,<br/>
> A solution set is:<br/>
> `[1, 7]`<br/>
> `[1, 2, 5]`<br/>
> `[2, 6]`<br/>
> `[1, 1, 6]`<br/>

<!-- more -->

---
## 分析

---
## 代码
``` python
# Definition for singly-linked list with a random pointer.
class Solution:

    def __init__(self):
        self.nums = None
        self.len_nums = 0
        self.total = 0
        self.combinations = [ ]

    def doCombinationSum(self, prefix, prefix_total, start, last, used):
        if start >= self.len_nums:
            return
        num = self.nums[start]

        result = True
        if num != last or used:   ###
            if prefix_total + num == self.total:
                new_prefix = prefix[:]
                new_prefix.append(num)
                self.combinations.append(new_prefix)
                return
            elif prefix_total + num < self.total:
                new_prefix = prefix[:]
                new_prefix.append(num)
                self.doCombinationSum(new_prefix, prefix_total + num, start + 1, num, True)
                self.doCombinationSum(new_prefix, prefix_total + num, start, num, True)
            else:
                return
        if num != last:       ###
            self.doCombinationSum(prefix, prefix_total, start + 1, num, False)
        return True

    # @param candidates, a list of integers
    # @param target, integer
    # @return a list of lists of integers
    def combinationSum(self, candidates, target):
        self.nums = candidates
        self.nums.sort()
        self.len_nums = len(self.nums)
        if 0 == self.len_nums:
            return [ ]
        self.total = target
        self.doCombinationSum([ ], 0, 0, -1, True)
        return self.combinations
```
