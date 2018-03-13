# 【LeetCode with Python】 70. Climbing Stairs
tags: Easy Problems, Dynamic Programming

## 题目
原题页面：<https://leetcode.com/problems/climbing-stairs/><br/>
本文地址：<<leetcode-with-python-domain>/climbing-stairs/><br/>
题目类型：Dynamic Programming<br/>
难度评价：Easy<br/>

> You are climbing a stair case. It takes *n* steps to reach to the top.<br/>
><br/>
> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?<br/>

<!-- more -->

---
## 分析
如果按照从右至左的逆序递归求解，其实就相当于搜索算法了，会造成子搜索过程的重复计算。搜索算法一般都可以用动态规划来替代，因此这里就用1D动态规划。<br/>
f(x)的求解，用归纳法进行推导。如果n=1，则f(1)=2；如果n=2，可以走1个1步，也可以走2个1步，则f(2)=2；如果n=3，如果一开始走1步，则有f(2)种走法，如果一开始走2步，则有f(1)种走法；如果n=4，如果一开始走1步，则右f(3)种走法，如果一开始有2步，则有f(2)种走法。由此可以推导出一个公式：f(x)=f(x-1)+f(x-2)，可以用数学归纳法进行证明。<br/>
然后可以发现，由于f(x)的求解只依赖于f(x-1)和f(x-2)，因此可以将空间复杂度缩小到int[3]。于是你就会进一步发现，这其实就是一个裴波拉契数列问题。<br/>

---
## 代码
``` python
class Solution:
    # @param n, an integer
    # @return an integer
    def climbStairs(self, n):
        if n <= 1:
            return 1
        arr = [1, 1, 0]
        for i in range(2, n + 1):
            arr[2] = arr[0] + arr[1]
            arr[0], arr[1] = arr[1], arr[2]
        return arr[2]
```
