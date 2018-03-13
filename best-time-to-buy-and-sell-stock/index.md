# 【LeetCode with Python】 121. Best Time to Buy and Sell Stock
tags: Medium Problems, Array, Dynamic Programming

## 题目
原题页面：<https://leetcode.com/problems/best-time-to-buy-and-sell-stock/><br/>
本文地址：<<leetcode-with-python-domain>/best-time-to-buy-and-sell-stock/><br/>
题目类型：Array Dynamic Programming<br/>
难度评价：Medium<br/>

> Say you have an array for which the *i*<sup>th</sup> element is the price of a given stock on day *i*.<br/>
><br/>
> If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.<br/>

<!-- more -->

---
## 分析
因为只允许完成一笔交易，因此只要遍历一次数组，找出最大的差值即可，不过必须是最大值出现在最小值的右边，所以不能简单地遍历数组找出最大值和最小值相减，因此这样可能造成的是“最大亏损”。正确的做法是：遍历一次数组，每遍历到一个元素时，都记录历史上出现过的最小值，然后计算当前遍历到的元素与历史最小值的差值，再记录历史上该差值的最大值即可。<br/>
据原题说明这属于动态规划题目，也许是所谓的一维动态规划？本人对动态规划的定义一直是不得要领……或许可以这样认为，凡是类似于数据归纳法这样，可以把问题分解为一个逐步的基于子问题的求解过程，就是动态规划。而子问题可以从几个维度分解，就是几维的动态规划。例如这里是从天数这一个维度上可以分解，就是一维动态规划。01背包问题，可以从背包容量和物品两个维度上划分，就是二维动态规划。<br/>

---
## 代码
``` python
class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
        if None == prices or len(prices) < 2:
            return 0
        min = prices[0]
        max_diff = 0
        for i in range(1, len(prices)):
            if prices[i - 1]  < min:
                min = prices[i - 1]
            cur_diff = prices[i] - min
            if cur_diff > max_diff:
                max_diff = cur_diff
        return max_diff
```
