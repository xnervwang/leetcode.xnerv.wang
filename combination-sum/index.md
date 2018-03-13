# 【LeetCode with Python】 39. Combination Sum
tags: Medium Problems, Array, Backtracking

## 题目
原题页面：<https://leetcode.com/problems/combination-sum/><br/>
本文地址：<http://leetcode.xnerv.wang/combination-sum/><br/>
题目类型：Array, Backtracking<br/>
难度评价：Medium<br/>
类似题目：[(M) Letter Combinations of a Phone Number](/letter-combinations-of-a-phone-number/), [(M) Combination Sum II](/combination-sum-ii/), [(M) Combinations](/combinations/), [(M) Combination Sum III](/combination-sum-iii/), [(M) Factor Combinations](/factor-combinations/)<br/>

> Given a set of candidate numbers (***C***) and a target number (***T***), find all unique combinations in ***C*** where the candidate numbers sums to ***T***.<br/>
><br/>
> The **same** repeated number may be chosen from ***C*** unlimited number of times.<br/>
><br/>
> **Note:**<br/>
><br/>
> 1. All numbers (including target) will be positive integers.<br/>
> 2. Elements in a combination (*a*<sub>1</sub>, *a*<sub>2</sub>, … , *a*<sub>k</sub>) must be in non-descending order. (ie, *a*<sub>1</sub> ≤ *a*<sub>2</sub> ≤ … ≤ *a*<sub>k</sub>).<br/>
> 3. The solution set must not contain duplicate combinations.<br/>
><br/>
> For example, given candidate set `2,3,6,7` and target `7`,<br/>
><br/>
> A solution set is:<br/>
> `[7]`<br/>
> `[2, 2, 3]`<br/>

<!-- more -->

---
## 分析
比较经典的递归回溯和组合问题。每个元素可以被使用多次，注意参数传入的set可能不是有序的，为确保万一先sort吧。这道题有两个值得思考的地方：<br/>
为什么不能用动态规划来解决这个问题？什么样的题可以用动态规划，动态规划究竟是什么，这个定义上的问题一直困扰着本人。但是至少可以确定一点，动态规划是用来解决最优化问题的，而不是组合问题。例如如果这道题改为，从集合中挑选出一个子集合，使其最接近于给出的target值，但是又不能超过target值，那这道题就是动态规划中典型的背包问题了。（好像不太对，像Interleaving String这个DP问题就是一个排列问题，而不是一个优化问题。DP问题可能得是一个可迭代分解的问题。）<br/>
无限递归问题。注意代码中的used变量，因为set中的值可以被使用多次。。。<br/>
另外注意题目说的是“a set of candidate numbers”，既然是set，说明numbers中是没有重复元素的。<br/>
（本题感觉理解得还不是很清楚）<br/>

---
## 代码
``` python
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
        # 只有当第一次考察该元素，或虽然不是第一次考察该元素，但是该元素上一轮已经被采用，才能继续下去
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
        # 决定不采用该元素并且将索引+1，只能发生在第一次考察该元素的时候，否则会有重复组合加入
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
