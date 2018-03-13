# 【LeetCode with Python】 26. Remove Duplicates from Sorted Array
tags: Easy Problems, Array, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/remove-duplicates-from-sorted-array/><br/>
本文地址：<http://leetcode.xnerv.wang/remove-duplicates-from-sorted-array/><br/>
题目类型：Array, Two Pointers<br/>
难度评价：Easy<br/>

> Given a sorted array, remove the duplicates in place such that each element appear only *once* and return the new length.<br/>
><br/>
> Do not allocate extra space for another array, you must do this in place with constant memory.<br/>
><br/>
> For example,<br/>
> Given input array *nums* = `[1,1,2]`,<br/>
><br/>
> Your function should return length = `2`, with the first two elements of *nums* being `1` and `2` respectively. It doesn't matter what you leave beyond the new length.<br/>

<!-- more -->

---
## 分析
有序数组的去重。关键在于下标操作，不要每次删除元素都整体移动后面的元素。<br/>

---
## 代码
``` python
class Solution:
    # @param a list of integers
    @return an integer
    def removeDuplicates(self, A):
    if None == A:
        return 0
    len_A = len(A)
    if len_A <= 1:
        return len_A

    m = 0
    n = 1
    while n < len_A:
        if A[m] != A[n]:
        m += 1
        if m != n:
            A[m] = A[n]
        n += 1
    return m + 1
```
