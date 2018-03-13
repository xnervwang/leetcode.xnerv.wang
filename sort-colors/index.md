# 【LeetCode with Python】 75. Sort Colors
tags: Medium Problems, Array, Two Pointers, Sort

## 题目
原题页面：<https://oj.leetcode.com/problems/sort-colors/><br/>
本文地址：<http://leetcode.xnerv.wang/sort-colors/><br/>
题目类型：Array, Two Pointers, Sort<br/>
难度评价：Medium<br/>
类似题目：[(M) Sort List](/sort-list/), [(M) Wiggle Sort](/wiggle-sort/)<br/>

> Given an array with *n* objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.<br/>
><br/>
> Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.<br/>
><br/>
> **Note:**<br/>
> You are not suppose to use the library's sort function for this problem.<br/>
><br/>
> **Follow up:**<br/>
> A rather straight forward solution is a two-pass algorithm using counting sort.<br/>
> First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.<br/>
><br/>
> Could you come up with an one-pass algorithm using only constant space?<br/>

<!-- more -->

---
## 分析
定义两个两头的下标left和right，i从左至右遍历数组，发现0就和left交换（同时left+=1），发现2就和right交换（同时right-=1）。这样就能确保下标 < left的元素都是0，而下标 > right的元素都是2。<br/>
还可以进行进一步的优化，left指针每次都移动到一个不是0的位置，right指针每次都移动到一个不是2的位置，这样也许可以减少一些交换次数。<br/>

---
## 代码
``` python
class Solution:
    # @param A a list of integers
    # @return nothing, sort in place
    def sortColors(self, A):
        len_A = len(A)
        if 1 == len(A):
            return
        left = 0
        right = len_A - 1
        i = 0
        while i <= right:
            if 0 == A[i]:
                if left == i:
                    i += 1
                else:
                    A[left], A[i] = A[i], A[left]
                left += 1
            elif 1 == A[i]:
                i += 1
            else:
                if right == i:
                    i += 1
                else:
                    A[right], A[i] = A[i], A[right]
                right -= 1
```
