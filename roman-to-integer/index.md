# 【LeetCode with Python】 13. Roman to Integer
tags: Easy Problems, Math, String

## 题目
原题页面：<https://leetcode.com/problems/roman-to-integer/><br/>
本文地址：<http://leetcode.xnerv.wang/roman-to-integer/><br/>
题目类型：Math, String<br/>
难度评价：Easy<br/>
类似题目：[(M) Integer to Roman](/integer-to-roman/)<br/>

> Given a roman numeral, convert it to an integer.<br/>
><br/>
> Input is guaranteed to be within the range from 1 to 3999.<br/>

<!-- more -->

---
## 分析
将一个罗马数值字符串转化为相应的int。<br/>
此题跟Integer to Roman有异曲同工之蛋疼，对于不熟悉罗马数字的童鞋就是一个噩梦。整体来说，罗马数字中的字符代表的数值大小，一般是从左至右非严格递减的（也就是说可能相邻的两个字符相等），然后不停地累加就行了。但如果发生相邻的两个元素，左边的字符比右边的字符代表的数值小，就需要减去左右这个字符代表的数值。如IV就是5-4=1，所以CIV就是100-1+5=104。<br/>
空间复杂度O(N)。时间复杂度O(N)。<br/>
注意IV等这类特殊情况。<br/>

---
## 代码
``` python
class Solution:
    # @return an integer
    def romanToInt(self, s):
        digits = { "I":1, "V":5, "X":10, "L":50, "C":100, "D":500, "M":1000 }
        len_s = len(s)
        num = 0
        for i in range(0, len_s - 1):
            cur = digits[s[i]]
            next = digits[s[i + 1]]
            if cur >= next:
                num += cur
            else:
                num -= cur
        num += digits[s[len_s - 1]]
        return num
```
