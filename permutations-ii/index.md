# 【LeetCode with Python】 47. Permutations II
tags: Medium Problems, Backtracking

## 题目
原题页面：<https://leetcode.com/problems/permutations-ii/><br/>
本文地址：<http://leetcode.xnerv.wang/permutations-ii/><br/>
题目类型：Backtracking<br/>
难度评价：Medium<br/>
类似题目：[(M) Next Permutation](/next-permutation/), [(M) Permutations](/permutations/), [(M) Palindrome Permutation II](/palindrome-permutation-ii/)<br/>

> Given a collection of numbers that might contain duplicates, return all possible unique permutations.<br/>
><br/>
> For example,<br/>
> `[1,1,2]` have the following unique permutations:<br/>
> `[1,1,2]`, `[1,2,1]`, and `[2,1,1]`.<br/>

<!-- more -->

---
## 分析
与Permutations在处理上的唯一区别是，对于重复元素，不去尝试调换，而是直接skip，避免出现重复的排列。<br/>

---
## 代码
``` python
class Solution:
    def doPermuteUnique(self, num_list):
        if 1 == len(num_list):
            return [ num_list ]
        res_list = [ ]
        for i in range(0, len(num_list)):
            if i > 0 and num_list[0] == num_list[i]:
                continue
            num_list[0], num_list[i] = num_list[i], num_list[0]
            sub_res_list = self.doPermuteUnique(num_list[1:])
            list_head = [ num_list[0] ]
            new_list = [ list_head + list for list in sub_res_list]
            res_list.extend(new_list)
        return res_list

    # @param num, a list of integer
    # @return a list of lists of integers
    def permuteUnique(self, num):
        num.sort()
        return self.doPermuteUnique(num)
```
