# 【LeetCode with Python】 1. Two Sum
tags: Medium Problems, Array, Hash Table

## 题目
原题页面：<https://leetcode.com/problems/two-sum/><br/>
本文地址：<<leetcode-with-python-domain>/two-sum/><br/>
题目类型：Array, Hash Table<br/>
难度评价：Medium<br/>
类似题目：[(M) 3Sum](/3sum/), [(M) 4Sum](/4sum/), [(M) Two Sum II - Input array is sorted](/two-sum-ii-input-array-is-sorted/), [(E) Two Sum III - Data structure design](/two-sum-iii-data-structure-design/)<br/>

> Given an array of integers, find two numbers such that they add up to a specific target number.<br/>
><br/>
> The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.<br/>
><br/>
> You may assume that each input would have exactly one solution.<br/>
><br/>
> **Input:** numbers={2, 7, 11, 15}, target=9<br/>
> **Output:** index1=1, index2=2<br/>

<!-- more -->

---
## 分析
给定一个数列（注意不一定有序），和一个指定的数值target。从这个数列中找出两个数相加刚好等于target，要求给出这两个数的下标（注意数列下标是从1而不是从0开始）。<br/>
首先将数列排序。由于最后要得求的是两个数的原有下标，而不是两个数本身，因此要用一个新的对象Item来封装原有数列元素，并记录该元素的原有下标。排序是针对数列元素本身数值的，分别用一个index1指针和一个index2指针指向排序后的数列的首位，如果指向的两个数相加的和等于target，则搜索结束；如果和小于target，则由于index2此时指向的已经是数组中的最大数了，因此只能令index1向右移动一次；如果和大于target，则由于此时index1已经指向数组中的最小数了，因此只能令index2向左移动一次。用一个循环重复上述过程，直到和等于target宣告搜索成功，或者index1>=index2宣告搜索失败。<br/>
空间复杂度O(n)，因为构造了一个新的Item序列。时间复杂度方面，如果假设Python的sort算法是用的快速排序的话，那排序的时间复杂度为O(n\*logn)，搜索过程的时间复杂度为O(n)，因此总的时间复杂度为O(n*logn)。<br/>
注意给的数列也许长度为0，这样无论target是多少都是搜索失败。而且题目中给的example明显是是在误导人，不仔细看误以为数列原本就有序。此外，数列下标是从1而不是从0开始的。<br/>
但是这种算法的前提要先进行一次排序，看起来总是有点不舒服，是不是有更好的算法呢？<br/>
（哈希表可以将时间复杂度降低到O(n)，另外好像编程之美中有这道题目？)<br/>

---
## 代码
``` python
class Solution:

    class Item:
        def __init__(self, value, index):
            self.value = value
            self.index = index

    # @return a tuple, (index1, index2)
    def twoSum(self, num, target):
        len_num = len(num)
        if 0 == len_num:
            return (-1, -1)

        items = [Solution.Item(value, 0) for value in num]
        for i in range(0, len_num):
            items[i].index = i + 1
        items.sort(lambda x, y: cmp(x.value, y.value))
        index1 = 0
        index2 = len_num - 1
        is_find = False
        while index1 < index2:
            total = items[index1].value + items[index2].value
            if total < target:
                index1 += 1
            elif total > target:
                index2 -= 1
            else:
                is_find = True
                break
        (index1, index2) = (index1, index2) if items[index1].index <= items[index2].index else (index2, index1)
        return (items[index1].index, items[index2].index) if is_find else (-1, -1)
```
