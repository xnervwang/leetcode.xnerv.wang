# 【LeetCode with Python】 53. Maximum Subarray
tags: Medium Problems, Divide and Conquer, Array, Dynamic Programming

## 题目
原题页面：<https://leetcode.com/problems/maximum-subarray/><br/>
本文地址：<<leetcode-with-python-domain>/maximum-subarray/><br/>
题目类型：Divide and Conquer, Array, Dynamic Programming<br/>
难度评价：Medium<br/>
类似题目：[(M) Best Time to Buy and Sell Stock](/best-time-to-buy-and-sell-stock/), [(M) Maximum Product Subarray](/maximum-product-subarray/)<br/>

> Find the contiguous subarray within an array (containing at least one number) which has the largest sum.<br/>
><br/>
> For example, given the array `[-2,1,-3,4,-1,2,1,-5,4]`,<br/>
> the contiguous subarray `[4,-1,2,1]` has the largest sum = `6`.<br/>
><br/>
> **More practice:**<br/>
><br/>
> If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.<br/>

<!-- more -->

---
## 分析
找最大和连续子数组，也是经典题目之一。和Gas Station有点类似的地方是，如果当前的子序列加入第k个元素后，sum小于0（首先说明k本身小于0），则这个子序列的sum对后续的k+1是无益的。而且即使从这个子序列中移除掉部分最左边的元素，也是没有用的，因为最左边的元素的总和一定是大于0的，移除掉会更差。所以此时不如从第k+1个元素从0开始重新sum。<br/>
可以想象一副不规则的波形图，sum就是从x轴的某一点开始的面积图。x轴上方的是有效面积，x轴下方的负数面积。<br/>

---
## 代码
``` python
class Solution:

    # @param A, a list of integers
    # @return an integer
    def maxSubArray(self, A):

        len_A = len(A)
        if 1 == len_A:
            return A[0]

        max = None
        sum = 0
        for n in range(0, len_A):
            sum += A[n]
            if None == max or sum > max:
                max = sum
            if sum < 0:
                sum = 0
                continue

        return max
```
