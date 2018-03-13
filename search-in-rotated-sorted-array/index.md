# 【LeetCode with Python】 33. Search in Rotated Sorted Array
tags: Hard Problems, Array, Binary Search

## 题目
原题页面：<https://oj.leetcode.com/problems/search-in-rotated-sorted-array/><br/>
本文地址：<<leetcode-with-python-domain>/search-in-rotated-sorted-array/><br/>
题目类型：Array, Binary Search<br/>
难度评价：Hard<br/>
类似题目：[(M) Search in Rotated Sorted Array II](/search-in-rotated-sorted-array-II/), [(M) Find Minimum in Rotated Sorted Array](/find-minimum-in-rotated-sorted-array/)<br/>

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.<br/>
><br/>
> (i.e., `0 1 2 4 5 6 7` might become`4 5 6 7 0 1 2`).<br/>
><br/>
> You are given a target value to search. If found in the array return its index, otherwise return -1.<br/>
> You may assume no duplicate exists in the array.<br/>

<!-- more -->

---
## 分析
二分查找的一个变种。整个数组由两个有序的子序列构成，且左子序列中的每个元素都>,右子序列中的每个元素。<br/>
如果每次A[left]<=A[right]，则说明当前段位于同一个有序子序列中。否则说明位于两个不同的有序子序列中，此时以mid为界，将当前段拆成两个子段，再递归这个过程。<br/>
题目中说明了数组中没有重复元素，因为有重复元素的情况下，上述算法可能会有问题。例如，序列是[4 5 6 7 0 3 4]，寻找的元素是3，则第一次时因为mid是7，则会进入左侧段中查找，则显然是找不到3的。<br/>

---
## 代码
``` python
class Solution:

    def doSearch(self, A, left, right, target):
        len_A = right - left + 1
        if 0 == len_A:
            return -1
        elif 1 == len_A:      ###
            return left if target == A[left] else -1
        if A[left] < A[right]:
            while left <= right:
                mid = (left + right) / 2
                if A[mid] < target:
                    left = mid + 1
                elif A[mid] > target:
                    right = mid - 1
                else:
                    return mid
        else:
            mid = (left + right) / 2
            left_result = self.doSearch(A, left, mid, target)
            if -1 != left_result:
                return left_result
            else:
                right_result = self.doSearch(A, mid + 1, right, target)
                if -1 != right_result:
                    return right_result
        return -1

    # @param A, a list of integers
    # @param target, an integer to be searched
    # @return an integer
    def search(self, A, target):
        len_A = len(A)
        return self.doSearch(A, 0, len(A) - 1, target)
```
