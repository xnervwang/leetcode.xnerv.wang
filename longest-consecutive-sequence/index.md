# 【LeetCode with Python】 128. Longest Consecutive Sequence
tags: Hard Problems, Array

## 题目
原题页面：<https://leetcode.com/problems/longest-consecutive-sequence/><br/>
本文地址：<http://leetcode.xnerv.wang/longest-consecutive-sequence/><br/>
题目类型：Array<br/>
难度评价：Hard<br/>

> Given an unsorted array of integers, find the length of the longest consecutive elements sequence.<br/>
><br/>
> For example,<br/>
> Given `[100, 4, 200, 1, 3, 2]`,<br/>
> The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.<br/>
><br/>
> Your algorithm should run in O(*n*) complexity.<br/>

<!-- more -->

---
## 分析
给定一个不一定有序的int序列，从里面找出一些能够构成一个新序列的数字，要求这些数字是连续的，并且新序列能足够长。<br/>
先对原序列排序，然后再遍历一次找最长连续序列这种做法是最直观的，时间复杂度是O(n*logn)+O(n)=O(n*log(n))，显然不满足本题要求O(n)复杂度的要求（话说原题要求的这个O(n)复杂度是仅指时间复杂度，还是同时要求时间复杂度和空间复杂度？估计是后者）。所以用一个hashmap，首先遍历原序列，以每个元素值作为key，True作为value插入到hashmap中。然后就可以遍历这个hashmap中的每个元素，试图去搜索这个元素左右连续的元素是否存在于hashmap中，从而去找出最长的连续序列。同时注意将搜索过的元素的Value置为False，避免对已经搜索过的连续序列中的元素再重复搜索。<br/>
空间复杂度O(n)。时间复杂度O(n)。由于Python中的字典就是用hash表实现的，因此这里就暂用字典代替hash表。<br/>
注意避免重复搜索同一连续序列中的其它元素。<br/>
总的来说这种算法比较难想到，排序后再遍历的算法比较直观，可能会在第一时间想到。<br/>

---
## 代码
``` python
class Solution:
    # @param num, a list of integer
    # @return an integer
    def longestConsecutive(self, num):
        hashmap = { }
        for i in num:
            hashmap[i] = True
        max_n = 0
        for k, v in hashmap.items():
            if not v:
                continue
            left = k - 1
            right = k + 1
            while hashmap.has_key(left) and hashmap[left]:
                hashmap[left] = False
                left -= 1
            while hashmap.has_key(right) and hashmap[right]:
                hashmap[right] = False
                right += 1
            n = right - left - 1
            if n > max_n:
                max_n = n
        return max_n
```
