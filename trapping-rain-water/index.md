# 【LeetCode with Python】 42. Trapping Rain Water
tags: Hard Problems, Array, Stack, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/trapping-rain-water/><br/>
本文地址：<http://leetcode.xnerv.wang/trapping-rain-water/><br/>
题目类型：Array, Stack, Two Pointers<br/>
难度评价：Hard<br/>
类似题目：[(M) Container With Most Water](/container-with-most-water/), [(M) Product of Array Except Self](/product-of-array-except-self/)<br/>

> Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.<br/>
><br/>
> For example,<br/>
> Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return `6`.<br/>
><br/>
> ![rainwatertrap](http://www.leetcode.com/wp-content/uploads/2012/08/rainwatertrap.png)<br/>
> <p style="font-size: 11px">The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!</p><br/>

<!-- more -->

---
## 分析
将一个数列看成是一堆高低不一的蓄水墙，数值即这面墙的高度，求总的蓄水最大量。其实题目中的图就已经一目了然了，无需过多文字说明。<br/>
针对某一个x点，决定其蓄水量应该是该点左右两边分别出现过的最高的墙中的最小者决定的。例如，针对A=[0,1,0,2,1,0,1,3,2,1,2,1]这个例子，A[4]=1这一点，其左边出现过的最高墙是A[3]=2，其右边出现过的最高墙是A[7]=3，因此两者中的最小者就就是A[3]=2，因此A[4]的蓄水高度就是A[3]-A[4]=1，乘以底边1，即A[4]蓄水量为1。<br/>
针对每一个点去单独寻找这个最小值显然是不合理的，这样时间复杂度就是O(n*n)了。申请一个与原数组A等长的数组max_heights用来记录每个点的最大蓄水量，首先从左至右遍历一次A，记录当前遇到过的最大值，依次填入到max_heights中。然后再从右至左遍历一次A，也记录当前遇到过的最大值，与max_heights中对应位置的值进行比较，如果比max_heights中对应的值小，则替换掉max_heights中的值。通过这种方法，就能用2次时间复杂度为O(n)的遍历找出每个点的蓄水量，然后遍历max_heights，如果比A中对应的数值大的话，就累加其差值，最后得到的就是蓄水总量。也就是说，如果A中数值对max_heights中对应数值大，说明这个点无法蓄水。<br/>
空间复杂度为O(n)，时间复杂度为O(n)。<br/>

---
## 代码
``` python
class Solution:
    # @param A, a list of integers
    # @return an integer
    def trap(self, A):
        len_A = len(A)
        if 1 == len_A:
            return 0
        max_heights = [0] * len_A
        left_max = 0
        for i in range(0, len_A):
            if A[i] > left_max:
                left_max = A[i]
            max_heights[i] = left_max
        right_max = 0
        for i in range(len_A - 1, -1, -1):
            if A[i] > right_max:
                right_max = A[i]
            if right_max < max_heights[i]:
                max_heights[i] = right_max
        result = 0
        for i in range(0, len_A):
            if max_heights[i] > A[i]:
                result += (max_heights[i] - A[i])
        return result
```
