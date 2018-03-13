# 【LeetCode with Python】 17. Letter Combinations of a Phone Number
tags: Medium Problems, Backtracking, String

## 题目
原题页面：<https://leetcode.com/problems/letter-combinations-of-a-phone-number/><br/>
本文地址：<http://leetcode.xnerv.wang/letter-combinations-of-a-phone-number/><br/>
题目类型：Backtracking, String<br/>
难度评价：Medium<br/>
类似题目：[(M) Generate Parentheses](/generate-parentheses/), [(M) Combination Sum](/combination-sum/)<br/>

> Given a digit string, return all possible letter combinations that the number could represent.<br/>
><br/>
> A mapping of digit to letters (just like on the telephone buttons) is given below.<br/>
> ![200px-Telephone-keypad2](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)<br/>
><br/>
>> **Input:** Digit string "23"<br/>
>> **Output:** ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].<br/>
><br/>
> **Note:**<br/>
> Although the above answer is in lexicographical order, your answer could be in any order you want.<br/>

<!-- more -->

---
## 分析
原题标注类型递归回溯，可能是希望用递归回溯来解决这个问题。但其实这是个尾递归，所以可以直接用循环代替。<br/>

---
## 代码
``` python
class Solution:
    # @return a list of strings, [s1, s2]
    def letterCombinations(self, digits):
        map = {
               "0":  (),
               "1":  (),
               "2": ("a", "b", "c"),
               "3": ("d", "e", "f"),
               "4": ("g", "h", "i"),
               "5": ("j", "k", "l"),
               "6": ("m", "n", "o"),
               "7": ("p", "q", "r", "s"),
               "8": ("t", "u", "v"),
               "9": ("w", "x", "y", "z")
               }
        result1 = [ "" ]
        result2 = [ ]
        for ch in digits:
            list = map[ch]
            if 0 == len(list):
                continue
            for str in result1:
                for suffix in list:
                    result2.append(str + suffix)
            result1 = result2
            result2 = [ ]
        return result1
```
