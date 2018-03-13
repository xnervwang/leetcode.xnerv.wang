# 【LeetCode with Python】 57. Insert Interval
tags: Hard Problems, Array, Sort

## 题目
原题页面：<https://leetcode.com/problems/insert-interval/><br/>
本文地址：<<leetcode-with-python-domain>/insert-interval/><br/>
题目类型：Array, Sort<br/>
难度评价：Hard<br/>
类似题目：[(H) Merge Intervals](/merge-intervals/)<br/>

> Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).<br/>
><br/>
> You may assume that the intervals were initially sorted according to their start times.<br/>
><br/>
> **Example 1:**<br/>
> Given intervals `[1,3],[6,9]`, insert and merge `[2,5]` in as `[1,5],[6,9]`.<br/>
><br/>
> **Example 2:**<br/>
> Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` in as `[1,2],[3,10],[12,16]`.<br/>
><br/>
> This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.<br/>

<!-- more -->

---
## 分析
首先要找到newInterval在已有数组中的位置。有三种可能：<br/>

1. newInterval与已有数组没有交集，位于数组最左端，即left_index=0，right_index=-1。此时直接将newInterval插入到数组头部即可。<br/>
2. newInterval与已有数组没有交集，位于数组最右端，即left_index=-1。此时直接将newInterval插入到数组尾部即可。<br/>
3. newInterval与已有数组有交集，这是最普遍的一种情况。newInterval可能是和数组中已有的一个interval有交集，也有可能是跨了几个interval。此时left_index表示数组中右值>=newInterval的左值的最大的interval（约定在数轴上越靠右的interval最大），而right_index表示数组中左值<=newInterval的右值的最小的interval，这样就能界定出newInterval影响的数组范围。凡是在影响范围之外的数组部分，直接原样加入到结果数组中即可。而在影响范围之内的数组部分，需要和newInterval合成一个单独的interval（即代码中的add_interval），然后加入到结果数组中。<br/>

---
## 代码
``` python
class Solution:
    # @param intervals, a list of Intervals
    # @param newInterval, a Interval
    # @return a list of Interval
    def insert(self, intervals, newInterval):

        len_intervals = len(intervals)
        if 0 == len_intervals:
            return [ newInterval ]

        left_index = -1
        right_index = -1
        find_left = False
        for m in range(0, len_intervals):
            if not find_left and newInterval.start <= intervals[m].end:
                find_left = True
                left_index = m
            if find_left:
                if newInterval.end >= intervals[m].start:
                    right_index = m

        if -1 == left_index:        ###
            intervals.append(newInterval)
            return intervals
        new_intervals = [ ]
        for m in range(0, left_index):
            new_intervals.append(intervals[m])
        add_interval = None
        start_index = -1
        if -1 != right_index:
            add_interval = Interval(min(newInterval.start, intervals[left_index].start), max(newInterval.end, intervals[right_index].end))
            start_index = right_index + 1
        else:      ###
            add_interval = newInterval
            start_index = left_index
        new_intervals.append(add_interval)
        for m in range(start_index, len_intervals):
            new_intervals.append(intervals[m])

        return new_intervals
```
