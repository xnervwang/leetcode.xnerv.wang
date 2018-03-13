# 【LeetCode with Python】 135. Candy
tags: Hard Problems, Greedy

## 题目
原题页面：<https://leetcode.com/problems/candy/><br/>
本文地址：<<leetcode-with-python-domain>/candy/><br/>
题目类型：Greedy<br/>
难度评价：Hard<br/>

> There are *N* children standing in a line. Each child is assigned a rating value.<br/>
><br/>
> You are giving candies to these children subjected to the following requirements:<br/>
><br/>
> * Each child must have at least one candy.<br/>
> * Children with a higher rating get more candies than their neighbors.<br/>
><br/>
> What is the minimum candies you must give?<br/>

<!-- more -->

---
## 分析
贪婪法。初始化一个大小为N的数组，元素都是1，表示每个人至少有一个糖果。然后进行两遍贪婪处理：<br/>

1. 首先先从左往右遍历，如果一个人的排名高于左侧的人，要比左侧的人多一个糖果。<br/>
2. 接着从右往左遍历，如果一个人的排名高于右侧的人，则至少要比右侧的人多一个糖果。当然如果该人的糖果本来就已经比右侧多，就无需多管了。<br/>

（有意思的是，如何证明贪婪法得到的是最优解？）<br/>

---
## 代码
``` python
class Solution:
    # @param ratings, a list of integer
    # @return an integer
    def candy(self, ratings):
        len_r = len(ratings)
        if len_r <= 1:
            return len_r
        candys = [1] * len_r
        candys[0] = 1
        candys[len_r - 1] = 1
        for i in range(1, len_r):
            if ratings[i] > ratings[i - 1]:
                candys[i] = candys[i - 1] + 1
        for i in range(len_r - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candys[i] = max(candys[i + 1] + 1, candys[i])
        return sum(candys)
```
