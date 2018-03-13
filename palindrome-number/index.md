# 【LeetCode with Python】 9. Palindrome Number
tags: Easy Problems, Math

## 题目
原题页面：<https://leetcode.com/problems/palindrome-number/><br/>
本文地址：<<leetcode-with-python-domain>/palindrome-number/><br/>
题目类型：Math<br/>
难度评价：Easy<br/>
类似题目：[(E) Palindrome Linked List](/palindrome-linked-list/)<br/>

> Determine whether an integer is a palindrome. Do this without extra space.<br/>
><br/>
> **Some hints:**<br/>
><br/>
> Could negative integers be palindromes? (ie, -1)<br/>
><br/>
> If you are thinking of converting the integer to string, note the restriction of using extra space.<br/>
><br/>
> You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?<br/>
><br/>
> There is a more generic way of solving this problem.<br/>

<!-- more -->

---
## 分析
判断一个数值是否是回文。首先负数肯定不是回文，而0~9则是回文。基本的思路是每次对比数值开头的数字和结尾的数字，看是不是相等。结尾的数字可以通过对10取余得到，于是问题的关键就在于怎样取出开头的数字了。<br/>
注意不要去尝试将整个数值倒置，这样可能会造成溢出。（不过如果这个数值是回文的话，倒置也不会溢出就是了。但是有没有可能一个数值本来不是回文，倒置后溢出的结果反而等于原数值了？？？）<br/>

---
## 代码
``` python
class Solution:

    # @return a boolean
    def isPalindrome(self, x):
        if x < 0:
            return False
        if x < 10:
            return True
        div = 1
        val = x
        while True:
            val = int(val / 10)
            if val > 0:
                div *= 10
            else:
                break

        while div > 0:
            left = int(x / div)
            right = int(x % 10)
            if left != right:
                return False
            x = x % div
            x = x / 10
            div = int(div / 100)
        return True
```
