# 【LeetCode with Python】 62. Unique Paths
tags: Medium Problems, Array, Dynamic Programming

## 题目
原题页面：<https://leetcode.com/problems/unique-paths/><br/>
本文地址：<<leetcode-with-python-domain>/unique-paths/><br/>
题目类型：Array, Dynamic Programming<br/>
难度评价：Medium<br/>
类似题目：[(M) Unique Paths II](/unique-paths-ii/), [(M) Minimum Path Sum](/minimum-path-sum/), [(H) Dungeon Game](/dungeon-game/)<br/>

> A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).<br/>
><br/>
> The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).<br/>
><br/>
> How many possible unique paths are there?<br/>
><br/>
> ![robot_maze](http://leetcode.com/wp-content/uploads/2014/12/robot_maze.png)<br/>
> Above is a 3 x 7 grid. How many possible unique paths are there?<br/>
><br/>
> **Note:** *m* and *n* will be at most 100.<br/>

<!-- more -->

---
## 分析
用数学中的排列组合来解题，从(m+n)次选择中选出m次向下走。<br/>
这道题跟“n阶台阶，每次一步或两步，总共多少种走法”一样，也可以用动态规划解题，不过这里是二维动态规划，而后者是一维动态规划。Unique Paths还比较简单，所以可用排列组合快速解题，但是Unique Paths II这道题，就只能用动态规划了。<br/>

---
## 代码
``` python
class Solution:
    # @return an integer
    def uniquePaths(self, m, n):
        if 0 == m or 0 == n:
            return 1
        up = 1
        for i in range(m + n - 2, n - 1, -1):
            up *= i
        down = 1
        for j in range(1, m):
            down *= j
        return up / down
```
