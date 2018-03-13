# 【LeetCode with Python】 4. Median of Two Sorted Arrays
tags: Hard Problems, Divide and Conquer, Array, Binary Search, todo

## 题目
原题页面：<https://leetcode.com/problems/median-of-two-sorted-arrays/><br/>
本文地址：<http://leetcode.xnerv.wang/median-of-two-sorted-arrays/><br/>
题目类型：Divide and Conquer, Array, Binary Search<br/>
难度评价：Hard<br/>

> There are two sorted arrays *nums1* and *nums2* of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).<br/>

<!-- more -->

---
## 分析
找两个有序数列的“中位值”。发现LeetCode上还是有不少坑。如，这个题目说的有序数列其实是从小到大排列的，不需要我们像处理其它经常埋坑的题那样“以小人之心度君子之腹”地去先检查A和B是从小到大还是从大到小，甚至有可能A从小到大而B却从大到小。其次，这个“median”并不是指“中位数”，而是“中位值”，两者的区别是：当m+n为奇数时，这两个词是一个概念。而当m+n为偶数时，中位数可以指按大小排在最中间的那两个数，而中位**值**则是指这两个数的平均数。何其坑哉！<br/>

---
## 代码
``` python
class Solution:

    # @return a float
    def findMedianSortedArrays(self, A, B):

        len_a = len(A)
        len_b = len(B)
        len_total = len_a + len_b
        if 0 == len_total:
            return ''
        if 0 == len_a and 1 == len_b:
            return B[0]
        if 1 == len_a and 0 == len_b:
            return A[0]
        if 1 == len_a and 1 == len_b:
            return float(A[0] + B[0]) / 2

        median_index = len_total / 2
        is_odd = (1 == len_total % 2)

        index_a = -1
        index_b = -1
        median_num = 0
        for i in range(0, median_index + 1):
            if index_a + 1 < len_a and (index_b + 1 >= len_b or A[index_a + 1] <= B[index_b + 1]):
                index_a += 1
                last_median_num = median_num
                median_num = A[index_a]
            else:
                index_b += 1
                last_median_num = median_num
                median_num = B[index_b]

        if is_odd:
            median_num = median_num
        else:
            median_num = float(last_median_num + median_num) / 2

        return median_num
```
