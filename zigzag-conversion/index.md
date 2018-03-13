# 【LeetCode with Python】 6. ZigZag Conversion
tags: Easy Problems, String

## 题目
原题页面：<https://leetcode.com/problems/zigzag-conversion/><br/>
本文地址：<http://leetcode.xnerv.wang/zigzag-conversion/><br/>
题目类型：String<br/>
难度评价：Easy<br/>

> The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)<br/>
> `P---A---H---N`
> `A-P-L-S-I-I-G`<br/>
> `Y---I---R`
><br/>
> And then read line by line: `"PAHNAPLSIIGYIR"`<br/>
> Write the code that will take a string and make this conversion given a number of rows:<br/>
> `string convert(string text, int nRows);`<br/>
> `convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.<br/>

<!-- more -->

---
## 分析
下标计算处理，控制好循环条件，下标不要越界即可。<br/>

---
## 代码
``` python
class Solution:
    # @return a string
    def convert(self, s, nRows):
        if 1 == nRows:
            return s

        len_s = len(s)
        piece_len = 2 * (nRows - 1)

        result = ""
        index = 0
        while index < len_s:
            result += s[index]
            index += piece_len
        for m in range(1, nRows - 1):
            index = m
            while index < len_s:
                result += s[index]
                right_index = index + (nRows - m - 1) * 2
                if right_index < len_s:
                    result += s[right_index]
                index += piece_len
        index = nRows - 1
        while index < len_s:
            result += s[index]
            index += piece_len

        return result
```
