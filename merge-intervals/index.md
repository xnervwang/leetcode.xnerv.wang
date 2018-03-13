# 【LeetCode with Python】 56. Merge Intervals
tags: Hard Problems, Array, Sort

## 题目
原题页面：<https://leetcode.com/problems/merge-intervals/><br/>
本文地址：<<leetcode-with-python-domain>/merge-intervals/><br/>
题目类型：Array, Sort<br/>
难度评价：Hard<br/>
类似题目：[(H) Insert Interval](/insert-interval/), [(E) Meeting Rooms](/meeting-rooms/), [(M) Meeting Rooms II](/meeting-rooms-ii/)<br/>

> Given a collection of intervals, merge all overlapping intervals.<br/>
><br/>
> For example,<br/>
> Given `[1,3],[2,6],[8,10],[15,18]`,<br/>
> return `[1,6],[8,10],[15,18]`.<br/>

<!-- more -->

---
## 分析
合并相连的区间。基本思路是，**首先按起点start对所有区间排序**，然后通过一次遍历来合并相连的区间。<br/>

---
## 代码
``` python
class Interval:

    def __init__(self, s=0, e=0):
        self.start = s
        self.end = e

class Solution:

    # @param intervals, a list of Interval
    # @return a list of Interval
    def merge(self, intervals):

        if len(intervals) <= 1:
            return intervals

        intervals.sort(lambda x, y: cmp(x.start, y.start))
        new_intervals = [ ]
        last_interval = intervals[0]
        for i in range(1, len(intervals)):
            if intervals[i].start >= last_interval.start and intervals[i].start <= last_interval.end:
                if intervals[i].end >= last_interval.start and intervals[i].end <= last_interval.end:
                    pass
                else:
                    last_interval.end = intervals[i].end
            else:
                new_intervals.append(last_interval)
                last_interval = intervals[i]
        new_intervals.append(last_interval)

        return new_intervals
```
