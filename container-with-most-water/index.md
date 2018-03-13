# 【LeetCode with Python】 11. Container With Most Water
tags: Medium Problems, Array, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/container-with-most-water/><br/>
本文地址：<<leetcode-with-python-domain>/container-with-most-water/><br/>
题目类型：Array, Two Pointers<br/>
难度评价：Medium<br/>
类似题目：[(H) Trapping Rain Water](/trapping-rain-water/)<br/>

> Given *n* non-negative integers *a<sub>1</sub>*, *a<sub>2</sub>*, ..., *a<sub>n</sub>*, where each represents a point at coordinate (*i*, *a<sub>i</sub>*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *a<sub>i</sub>*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.<br/>
><br/>
> Note: You may not slant the container.<br/>

<!-- more -->

---
## 分析
贪婪法的思想，用两个指针从数组的左边和右边开始，向中间搜索。依据的理由有两点：<br/>
1、因为一开始底边长就已经是最大，两个指针向中间移动的时候，底边长只会变短，因此如果此时面积要变大的话，只能是两条高中的最短者比移动前的最短高更高，否则就无需考察，直接continue到下一次的循环。<br/>
2、因此，每次选择移动左指针还是右指针，优先选择当前高度最短的那个，以期寻找到更高的边。如果此时选择移动当前高度最高的那个，就有可能跳过了最优解。<br/>

---
## 代码
``` python
class Solution:
    # @return an integer
    def maxArea(self, height):
        len_height = len(height)
        if 1 == len_height:
            return 0
        max_area = 0
        left_index = 0
        right_index = len_height - 1
        while left_index < right_index:
            if height[left_index] < height[right_index]:
                area = (right_index - left_index) * height[left_index]
                left_index += 1
            else:
                area = (right_index - left_index) * height[right_index]
                right_index -= 1
            if area > max_area:
                    max_area = area
        return max_area
```
