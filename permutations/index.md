# 【LeetCode with Python】 46. Permutations
tags: Medium Problems, Backtracking

## 题目
原题页面：<https://leetcode.com/problems/permutations/><br/>
本文地址：<<leetcode-with-python-domain>/permutations/><br/>
题目类型：Backtracking<br/>
难度评价：Medium<br/>
类似题目：[(M) Next Permutation](/next-permutation/), [(M) Permutations II](/permutations-ii/), [(M) Permutation Sequence](/permutation-sequence/), [(M) Combinations](/combinations/)<br/>

> Given a collection of numbers, return all possible permutations.<br/>
><br/>
> For example,<br/>
> `[1,2,3]` have the following permutations:<br/>
> `[1,2,3]`, `[1,3,2]`, `[2,1,3]`, `[2,3,1]`, `[3,1,2]`, and `[3,2,1]`.<br/>

<!-- more -->

---
## 分析
一道递归回溯的题目，所以跟大多数递归回溯题目类似的解法。只有一点值得注意一下，由于需要从一个集合中挑选出元素，然后下一次递归从剩余的元素中继续挑选，所以必须能够记忆和区分出当前已经选出了哪些元素。这里的做法是每次把选择的元素与当前列表中第一个元素交换，然后将除第一个元素外的子列表传递给下一次递归作为其需要处理的当前列表。<br/>
另外，a collection of numbers也许是暗示了集合中不会有重复元素？至少对比[(M) Permutations II](/permutations-ii/)看来，本题的原意应该是没有重复元素的。<br/>

---
## 代码
``` python
class Solution:
    def doPermute(self, num_list):
        if 1 == len(num_list):
            return [ num_list ]
        res_list = [ ]
        for i in range(0, len(num_list)):
            num_list[0], num_list[i] = num_list[i], num_list[0]
            sub_res_list = self.doPermute(num_list[1:])
            list_head = [ num_list[0] ]
            new_list = [ list_head + list for list in sub_res_list]
            res_list.extend(new_list)
        return res_list

    # @param num, a list of integer
    # @return a list of lists of integers
    def permute(self, num):
        return self.doPermute(num)
```
