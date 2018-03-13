# 【LeetCode with Python】 38. Count and Say
tags: Easy Problems, String

## 题目
原题页面：<https://leetcode.com/problems/count-and-say/><br/>
本文地址：<<leetcode-with-python-domain>/count-and-say/><br/>
题目类型：String<br/>
难度评价：Easy<br/>
类似题目：[(M) Encode and Decode Strings](/encode-and-decode-strings/)<br/>

> The count-and-say sequence is the sequence of integers beginning as follows:<br/>
> `1, 11, 21, 1211, 111221, ...`<br/>
><br/>
> `1` is read off as `"one 1"` or `11`.<br/>
> `11` is read off as `"two 1s"` or `21`.<br/>
> `21` is read off as `"one 2`, then `one 1"` or `1211`.<br/>
><br/>
> Given an integer *n*, generate the *n*<sup>th</sup> sequence.<br/>
><br/>
> Note: The sequence of integers will be represented as a string.<br/>

<!-- more -->

---
## 分析
主要是计数的逻辑。每一轮，遇到一个不同的字符时，就结束到该轮的计数。但是需要注意的是最后一轮的计数，因为遇到的是字符串src的结尾，所以需要强制结束这一轮的计数，就类似于编译原理词法分析最后的那个$符号的作用。<br/>

---
## 代码
``` python
class Solution:

    def doCountAndSay(self, src):
        char = src[0]
        num = 0
        result = ""
        for c in src:
            if char == c:
                num += 1
            else:
                result += (str(num) + char)
                char = c
                num = 1
        result += (str(num) + char)
        return result

    # @return a string
    def countAndSay(self, n):
        if 0 == n:
            return ""
        elif 1 == n:
            return "1"
        result = "1"         # str is a keyword
        for i in range(1, n):
            result = self.doCountAndSay(result)
        return result
```
