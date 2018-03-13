# 【LeetCode with Python】 122. Best Time to Buy and Sell Stock II
tags: Medium Problems, Array, Greedy

## 题目
原题页面：<https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/><br/>
本文地址：<<leetcode-with-python-domain>/best-time-to-buy-and-sell-stock-ii/><br/>
题目类型：Array, Greedy<br/>
难度评价：Medium<br/>
类似题目：[(M) Best Time to Buy and Sell Stock](/best-time-to-buy-and-sell-stock/), [(H) Best Time to Buy and Sell Stock III](/best-time-to-buy-and-sell-stock-iii/), [(H) Best Time to Buy and Sell Stock IV](/best-time-to-buy-and-sell-stock-iv/)<br/>

> Say you have an array for which the *i*<sup>th</sup> element is the price of a given stock on day *i*.<br/>
><br/>
> Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).<br/>

<!-- more -->

---
## 分析
一开始还以为是找出序列中的最大值和最小值然后求差，这种错误的想法充分暴露了本人炒股属于把钱往里一丢就再也不管了的类型。其实这题体现的就是一个“低买高买”的贪婪思想，需要找到每一个递增的子序列，从而使利润最大化。<br/>

---
## 代码
``` python
class Solution:

    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
        len_prices = len(prices)
        if len_prices <= 1:
            return 0

        start = prices[0]
        index = 1
        income = 0
        total_income = 0
        while index < len_prices:
            cur = prices[index]
            if cur >= prices[index - 1]:
                income = cur - start
                index += 1
                if len_prices == index:
                    total_income += income
            else:
                total_income += income
                income = 0
                start = cur
                index += 1

        return total_income
```
