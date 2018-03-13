# 【LeetCode with Python】 149. Max Points on a Line
tags: Hard Problems, Hash Table, Math

## 题目
原题页面：<https://leetcode.com/problems/max-points-on-a-line/><br/>
本文地址：<http://leetcode.xnerv.wang/max-points-on-a-line/><br/>
题目类型：Hash Table, Math<br/>
难度评价：Hard<br/>

Given *n* points on a 2D plane, find the maximum number of points that lie on the same straight line.<br/>

<!-- more -->

---
## 分析
> 首先要找到newInterval在已有数组中的位置。有三种可能：<br/>
><br/>
> 这道题比较容易陷入一种思维定势。也就是，大家中学里都学过A，B，C三点共线的判断方法，即判断AB和BC的斜率相等。那么就每次选出两个点，然后去遍历其他点，看是否与这两个点共线，最后找出共线最多的点数。这个算法的时间复杂度是O(n<sup>3</sup>)。这种每次选三个点的做法，会造成大量的重复比较。从时间复杂度上来看，应该还有其它更好的方法。<br/>
> 更好的方法也就是，每次只挑出一个点，然后遍历其他点，计算与该点形成的斜率，然后统计到相应的map（字典）中，这样复杂度就降低到了O(n<sup>2</sup>)，因为Python的字典是用Hash表实现，所以理想情况下可以看成插入和查找的时间复杂度为O(1)。<br/>
另外，对于选定点A，另外两个共线点B和C是出现在A在同一侧（左侧或右侧），还是出现在不同侧，BA和BC的斜率都是相等的，结合笛卡尔坐标系可以看出这一点。<br/>
> 但是需要特别注意两种特殊点：<br/>
><br/>
> 1. 与当前考察点重合。这类点可以算入到任何其它斜率的直线上。如A点和B点形成30度斜率，C点和A点重合，那么30度斜率直线上至少就有A，B，C三个点。<br/>
> 2. 与当前考察点垂直。因为这种情况斜率无穷大，dx分母为0，不能进行计算斜率的除法操作，因此要单独计数。<br/>

---
## 代码
``` python
class Solution:
    # @param points, a list of Points
    # @return an integer
    def maxPoints(self, points):
        len_points = len(points)
        if len_points <= 1:
            return len_points
        max_count = 0
        for index1 in range(0, len_points):
            p1 = points[index1]
            gradients = {}
            infinite_count = 0
            duplicate_count = 0
            for index2 in range(index1, len_points):
                p2 = points[index2]
                dx = p2.x - p1.x
                dy = p2.y - p1.y
                if 0 == dx and 0 == dy:
                    duplicate_count += 1
                if 0 == dx:
                    infinite_count += 1
                else:
                    g = float(dy) / dx   # take care
                    gradients[g] = (gradients[g] + 1 if gradients.has_key(g) else 1)
            if infinite_count > max_count:
                max_count = infinite_count
            for k, v in gradients.items():
                v += duplicate_count
                if v > max_count:
                    max_count = v
        return max_count
```
