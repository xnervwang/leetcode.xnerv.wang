# 【LeetCode with Python】 12. Integer to Roman
tags: Medium Problems, Math, String

## 题目
原题页面：<https://leetcode.com/problems/integer-to-roman/><br/>
本文地址：<http://leetcode.xnerv.wang/integer-to-roman/><br/>
题目类型：Math, String<br/>
难度评价：Medium<br/>
类似题目：[(E) Roman to Integer](/roman-to-integer/), [(M) Integer to English Words](/integer-to-english-words/)<br/>

> Given an integer, convert it to a roman numeral.<br/>
><br/>
> Input is guaranteed to be within the range from 1 to 3999.<br/>

<!-- more -->

---
## 分析
将一个int转化为对应的罗马数字表示。<br/>
罗马数字还是挺复杂的，尤其是在和阿拉伯数字转换之时。建议可以看看维基百科，反正我是看晕了，最后找了前人的这题解法才算明白。<br/>
首先，罗马数字是不能表示负数和零的，所以遇到这样的阿拉伯数字时就直接返回空字符串吧。然后基本思路是，按照罗马数字从大到小的优先顺序，每次都从阿拉伯数字num中减去一个够减的罗马数字代表的数值，然后循环直到num为0为止。然后最大的问题来了，那就是罗马数字里像IV（4），XC（90）等这种，貌似还有一些惯例用法，像8是VIII而不是IIX，C的左边只能用X而不能用I等，复杂到了极点。我的建议是：罗马灭亡是有其缘由的，我们就不必在他们的文化上再纠结了。将单个罗马数字和惯例用法按数值从大到小排列，然后按照上面提到的基本思路来求解。<br/>
空间复杂度是O(n)。时间复杂度大约是O(n)？<br/>

---
## 代码
``` python
class Solution:
    # @return a string
    def intToRoman(self, num):
        if num <= 0:
            return ""
        digits = { "I":1, "V":5, "X":10, "L":50, "C":100, "D":500, "M":1000 }
        nums = (1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1)
        chs = ("M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I")
        len = 13
        s = ""
        while num > 0:
            for i in range(0, len):
                if num >= nums[i]:
                    num -= nums[i]
                    s += chs[i]
                    break
        return s
```
