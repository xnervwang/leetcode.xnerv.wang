# 【LeetCode with Python】 8. String to Integer (atoi)
tags: Easy Problems, Math, String

## 题目
原题页面：<https://leetcode.com/problems/string-to-integer-atoi/><br/>
本文地址：<http://leetcode.xnerv.wang/string-to-integer-atoi/><br/>
题目类型：Easy<br/>
难度评价：Math, String<br/>
类似题目：[(E) Reverse Integer](/reverse-integer/), [(H) Valid Number](/valid-number/)<br/>

> Implement **atoi** to convert a string to an integer.<br/>
><br/>
> **Hint:** Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.<br/>
><br/>
> **Notes:**<br/>
> It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.<br/>
><br/>
> **<font color="red">Update (2015-02-10):</font>**<br/>
> The signature of the `C++` function had been updated. If you still see your function signature accepts a `const char *</code>` argument, please click the reload button to reset your code definition.<br/>
><br/>
> **Requirements for atoi:**<br/>
><br/>
> The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.<br/>
><br/>
> The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.<br/>
><br/>
> If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.<br/>
><br/>
> If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.<br/>

<!-- more -->

---
## 分析
1. 正负号自然不用说，还要注意字符串开头允许任意长度的空格，结尾允许任意长度的非数字字符。<br/>
2. int为32位数据类型，当字符串代表的整数值超出int的表示范围时（大于int最大值，或小于int最小值），要能截断到int的最大值或最小值。但是如何判断当前的值已经大于int最大值或者小于int最小值，此时如果用int存储当前值的话，已经发生溢出而出错。当然，这里是用Python来解题的，整数变量的范围不止32位。但是如果是用C++结题呢？一般两种做法，一个是用更大的数据类型，如long long来存储当前值。还有一种办法，就是类似于下面的代码中的方法，就是直接用当前值的字符串，和int最大值最小值的字符串去进行字符串大小比较。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.max_int_bits = 32
        self.max_int_str = str(pow(2, self.max_int_bits - 1) - 1)
        self.min_int_str = str(pow(2, self.max_int_bits - 1))   # abs value, without sign
        self.max_int_len = len(self.max_int_str)
        self.min_int_len = len(self.min_int_str)

    # @return an integer
    def atoi(self, str):

        len_s = len(str)
        if 0 == len_s:
            return 0

        index = 0
        while index < len_s and ' ' == str[index]:
            index += 1
        sign = 1
        if index < len_s:
            if '+' == str[index]:
                sign = 1
                index += 1
            elif '-' == str[index]:
                sign = -1
                index += 1
        value = 0
        val_str = ''
        for i in range(index, len_s):
            ch = str[i]
            if ch >= '0' and ch <= '9':
                val_str += ch

                if len(val_str) > self.max_int_len or len(val_str) > self.min_int_len:
                    return int(self.max_int_str) if 1 == sign else -int(self.min_int_str)
                if len(val_str) >= self.max_int_len and val_str > self.max_int_str:
                    return int(self.max_int_str) if 1 == sign else -int(self.min_int_str)

                value = value * 10 + ord(ch) - ord('0')
                index += 1
            else:
                break

        return value * sign
```
