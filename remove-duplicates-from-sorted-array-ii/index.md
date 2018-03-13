# 【LeetCode with Python】 80. Remove Duplicates from Sorted Array II
tags: Medium Problems, Array, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/><br/>
本文地址：<<leetcode-with-python-domain>/remove-duplicates-from-sorted-array-ii/><br/>
题目类型：Array, Two Pointers<br/>
难度评价：Medium<br/>

> Follow up for "Remove Duplicates":<br/>
> What if duplicates are allowed at most *twice*?<br/>
><br/>
> For example,<br/>
> Given sorted array *nums* = `[1,1,1,2,2,3]`,<br/>
><br/>
> Your function should return length = `5`, with the first five elements of *nums* being `1`, `1`, `2`, `2` and `3`. It doesn't matter what you leave beyond the new length.<br/>

<!-- more -->

---
## 分析
和Remove Duplicates from Sorted Array类似，只是一个元素可以重复出现最多两次，因此可以模仿Remove Duplicates from Sorted List II的解法。<br/>

---
## 代码
``` python
class Solution:
    # @param a list of integers
    # @return an integer
    def removeDuplicates(self, A):
        if None == A:
            return 0
        len_A = len(A)
        if len_A <= 1:
            return len_A

        m = 0
        n = 1
        count = 1
        while n < len_A:
            if A[m] != A[n]:
                count = 1
                m += 1
                if m != n:
                    A[m] = A[n]
            elif count >= 2:
                count += 1
            else:
                m += 1
                count += 1
                if m != n:
                    A[m] = A[n]
            n += 1
        return m + 1
```
