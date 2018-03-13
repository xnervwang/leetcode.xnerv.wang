# 【LeetCode with Python】 134. Gas Station
tags: Medium Problems, Greedy

## 题目
原题页面：<https://leetcode.com/problems/gas-station/><br/>
本文地址：<<leetcode-with-python-domain>/gas-station/><br/>
题目类型：Greedy<br/>
难度评价：Medium<br/>

> There are *N* gas stations along a circular route, where the amount of gas at station *i* is `gas[i]`.<br/>
><br/>
> You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from station *i* to its next station (*i*+1). You begin the journey with an empty tank at one of the gas stations.<br/>
><br/>
> Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.<br/>
><br/>
> **Note:**<br/>
> The solution is guaranteed to be unique.<br/>

<!-- more -->

---
## 分析
基本解题思路是：先计算出一个“结余”数组，即当前车辆剩余油量，加上每一站可以补充的油量，减去从该站出发到下一站的消耗量，即每一站的“结余量”。一条合法的路线，当车辆处于中间的每一个点上，“结余量”都不能小于0。<br/>
不过有两种方法可以减小计算量，使得时间复杂度为O(n)，而不是暴力搜索时的O(n*n)。<br/>

一是假设当从A点出发，到D点时如果结余量小于0，则下一次的起点直接设置为D（其实应该可以设置为D的下一点E，这里为了程序逻辑处理简单就设为了D）。理由如下：A到C的累加和都>=0，而D应该是一个绝对值比这个累加和都大的负数，因此导致D点的结余量为负。<br/>
如果这时不把新的起点设置为D，而是设置为B，毫无疑问A>=0（否则在A点时就结余量为负了），既然A+B+C的结余量都不够D点消耗，则B+C更加不够D点消耗了。<br/>
如果此时新的起点设置为C，首先毫无疑问A+B>=0，否则A+B的结余量就不够C点消耗。既然A+B+C的结余量都不够D点消耗，则C点的结余量就更不够D点消耗了。<br/>
……<br/>
这可以看作：一条合法（或局部合法）的线路，其前缀之和总是一个非负数。如果当前点没有足够结余量可以通过，那去除任意长度的一个前缀，将更加不可能通过。<br/>

二是可以保存前缀之和中的最小值。因为题中线路是一个环形，而程序中是一个线性数组。当从数组中的某一点出发，到达数组尾部后，又要绕回数组头部，直到回到出发点。从一中已经可以保证尾部任何一个元素不会被重复在两次累加计算中出现，那么头部应该也可以这样避免被重复计算。用一个变量保存头部前缀的累加计算过程中出现过的最小和，则在某次累加计算过程中，只要尾部元素的总和结余量仍足够头部前缀最小和消耗，就说明这条线路是合法的（没问题？）。<br/>

---
## 代码
``` python
class Solution:
    # @param gas, a list of integers
    # @param cost, a list of integers
    # @return an integer
    def canCompleteCircuit(self, gas, cost):
        len_remain = len(gas)
        remain = [x for x in gas]
        for i in range(0, len_remain):
            remain[i] -= cost[i]
        total = 0
        start = 0
        prefix_min = 0
        prefix_tot = 0
        is_find = False
        for i in range(0, len_remain):
            prefix_tot += remain[i]
            if prefix_tot < prefix_min:
                prefix_min = prefix_tot
            total += remain[i]
            if total < 0:
                start = i + 1
                total = 0
                continue
            elif len_remain - 1 == i and total + prefix_min >= 0:
                is_find = True
                break
        return start if is_find else -1
```
