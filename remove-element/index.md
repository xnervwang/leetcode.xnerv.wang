# 【LeetCode with Python】 27. Remove Element
tags: Easy Problems, Array, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/remove-element/><br/>
本文地址：<<leetcode-with-python-domain>/remove-element/><br/>
题目类型：Array, Two Pointers<br/>
难度评价：Easy<br/>
类似题目：[(E) Remove Linked List Elements](/remove-linked-list-elements/), [(E) Move Zeroes](/move-zeroes/)<br/>

> Given an array and a value, remove all instances of that value in place and return the new length.<br/>
><br/>
> The order of elements can be changed. It doesn't matter what you leave beyond the new length.<br/>

<!-- more -->

---
## 分析
题目已经暗示可以将需要删除的元素移至数组末尾，因此用两个下标m和n，m用来从左至右遍历数组寻找该元素，n从右至左记录可以用来交换的尾部位置。<br/>

---
## 代码
``` python
class Solution:
    # @param    A       a list of integers
    # @param    elem    an integer, value need to be removed
    # @return an integer
    def removeElement(self, A, elem):
        if None == A:
            return A
        len_A = len(A)
        m = 0
        n = len_A - 1
        while m <= n:
            if elem == A[m]:
                if elem != A[n]:
                    A[m], A[n] = A[n], A[m]
                    m += 1
                    n -= 1
                else:
                    n -= 1
            else:
                m += 1
        return n + 1
```
