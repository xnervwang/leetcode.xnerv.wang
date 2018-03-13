# 【LeetCode with Python】 65. Valid Number
tags: Hard Problems, Math, String

## 题目
原题页面：<https://oj.leetcode.com/problems/valid-number/><br/>
本文地址：<<leetcode-with-python-domain>/valid-number/><br/>
题目类型：Math, String<br/>
难度评价：hard<br/>
类似题目：[(E) String to Integer (atoi)](/string-to-integer-atoi/)<br/>

> Validate if a given string is numeric.<br/>
><br/>
> Some examples:<br/>
> `"0"` => `true`<br/>
> `"   0.1  "` => `true`<br/>
> `"abc"` => `false`<br/>
> `"1 a"` => `false`<br/>
> `"2e10"` => `true`<br/>
><br/>
> **Note:** It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.<br/>

<!-- more -->

---
## 分析
有穷自动机DFA。话说这题用NFA可以解吗？NFA的使用局限是什么？<br/>

---
## 代码
``` python
class Solution:
    def getType(self, ch):
        if '^' == ch:
            return 0
        elif ' ' == ch:
            return 1
        elif '+' == ch or '-' == ch:
            return 2
        elif ch >= '0' and ch <= '9':
            return 3
        elif '.' == ch:
            return 4
        elif 'e' == ch:
            return 5
        elif '$' == ch:
            return 6
        else:
            return 7

    def getMap(self):
        map = (
               (0,     0,      1,      4,      2,     -1,     -1,     -1),      # 0: ^ / space
               (-1,     -1,     -1,     4,     2,     -1,    -1,     -1),      # 1: + / -
               (-1,     -1,     -1,     3,     -1,    -1,    -1,     -1),       # 2: .
               (-1,     10,    -1,     3,      -1,     7,    11,     -1),       # 3: num
               (-1,     10,    -1,     4,      5,      7,   11,    -1),       # 4: num
               (-1,     10,    -1,     6,     -1,     7,     11,     -1),      # 5: .
               (-1,     10,    -1,     6,      -1,     7,    11,     -1),       # 6: num
               (-1,     -1,    8,       9,      -1,    -1,    -1,     -1),       # 7: e
               (-1,     -1,    -1,     9,      -1,     -1,    -1,     -1),       # 8: + / 1
               (-1,     10,    -1,     9,      -1,    -1,     11,    -1),       # 9: num
               (-1,     10,    -1,    -1,     -1,     -1,    11,     -1)       # 10: space
               )
        return map

    # @param s, a string
    # @return a boolean
    def isNumber(self, s):
        map = self.getMap()
        state = 0
        after_s = "^" + s + "$"
        for ch in after_s:
            type = self.getType(ch)
            state = map[state][type]
            if -1 == state:
                break

        return 11 == state
```
