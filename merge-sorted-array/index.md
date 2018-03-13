# 【LeetCode with Python】 88. Merge Sorted Array
tags: Easy Problems, Array, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/merge-sorted-array/><br/>
本文地址：<<leetcode-with-python-domain>/merge-sorted-array/><br/>
题目类型：Array, Two Pointers<br/>
难度评价：Easy<br/>
类似题目：[(E) Merge Two Sorted Lists](/merge-two-sorted-lists/)<br/>

> Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.<br/>
><br/>
> **Note:**<br/>
> You may assume that *nums1* has enough space (size that is > greater or equal to *m* + *n*) to hold additional elements from *nums2*. The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.<br/>

<!-- more -->

---
## 分析
将一个有序数组B合并到另一个有序数组A。这题如果从数组头开始合并，则每一次都要整体移动数组A后面的元素，显然不是理想的方法。一种巧妙的做法是**从两个数组尾部开始合并，这样就避免了大面积的数组元素移动**。<br/>

---
## 代码
``` python
class Solution:
    # @param A  a list of integers
    # @param m  an integer, length of A
    # @param B  a list of integers
    # @param n  an integer, length of B
    # @return nothing
    def merge(self, A, m, B, n):
        if 0 == n:
            return A
        if 0 == m:
            for i in range(0, n):
                A[i] = B[i]
            return A

        index = m + n - 1
        indexA = m - 1
        indexB = n - 1
        while indexA >= 0 and indexB >= 0:
            if A[indexA] >= B[indexB]:
                A[index] = A[indexA]
                index -= 1
                indexA -= 1
            else:
                A[index] = B[indexB]
                index -= 1
                indexB -= 1
        if indexA >= 0:
            pass
        else:
            for i in range(0, indexB + 1):
                A[i] = B[i]
```
