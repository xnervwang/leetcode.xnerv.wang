# 【LeetCode with Python】 35. Search Insert Position
tags: Medium Problems, Array, Binary

## 题目
原题页面：<https://oj.leetcode.com/problems/search-insert-position/><br/>
本文地址：<http://leetcode.xnerv.wang/search-insert-position/><br/>
题目类型：Array, Binary Search<br/>
难度评价：Medium<br/>
类似题目：[(E) First Bad Version](/first-bad-version/)<br/>

> Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.<br/>
><br/>
> You may assume no duplicates in the array.<br/>
><br/>
> Here are few examples.<br/>
> `[1,3,5,6]`, 5 &#8594; 2
> `[1,3,5,6]`, 2 &#8594; 1
> `[1,3,5,6]`, 7 &#8594; 4
> `[1,3,5,6]`, 0 &#8594; 0

<!-- more -->

---
## 分析
二分查找的一个变种。如果找到了target，就返回下标（正常的二分查找逻辑），否则就返回插入的位置。二分查找容易搞晕的是到底是返回left还是right，注意到left最终一定停在target上，或停在target的“位置”的右边，所以显然找不到target时，应该返回left的下标作为插入位置。<br/>

---
## 代码
``` python
class Solution:
    # @param A, a list of integers
    # @param target, an integer to be inserted
    # @return integer
    def searchInsert(self, A, target):
        if None == A:
            return 0
        len_A = len(A)
        if target > A[len_A - 1]:
            return len_A
        if target < A[0]:
            return 0

        left = 0
        right = len_A - 1
        while left <= right:    # also can be left < right
            mid = (left + right) / 2
            if A[mid] < target:
                left = mid + 1
            elif A[mid] > target:
                right = mid - 1
            else:
                return mid
        return left
```
