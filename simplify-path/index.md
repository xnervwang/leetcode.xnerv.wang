# 【LeetCode with Python】 71. Simplify Path
tags: Medium Problems, Stack, String

## 题目
原题页面：<https://oj.leetcode.com/problems/simplify-path/><br/>
本文地址：<<leetcode-with-python-domain>/simplify-path/><br/>
题目类型：Stack, String<br/>
难度评价：Medium<br/>

> Given an absolute path for a file (Unix-style), simplify it.<br/>
><br/>
> For example,<br/>
> **path** = `"/home/"`, => `"/home"`<br/>
> **path** = `"/a/./b/../../c/"`, => `"/c"`<br/>
><br/>
> **Corner Cases:**<br/>
> * Did you consider the case where **path** = `"/../"`?<br/>
> * In this case, you should return `"/"`.<br/>
> * Another corner case is the path might contain multiple slashes `'/'` together, > such as `"/home//foo/"`.<br/>
> * In this case, you should ignore redundant slashes and return `"/home/foo"`.<br/>

<!-- more -->

---
## 分析
用栈分析Linux路径，得出最后的结果。需要注意的就是Corner Cases了，如果是Windows用的相对较多的同学，很可能就不会注意到这些细节。但实际上很多涉及路径的win32 API也支持这种Corner Cases。<br/>

---
## 代码
``` python
class Solution:
    # @param path, a string
    # @return a string
    def simplifyPath(self, path):
        stack = [ ]
        toks = path.split("/")
        stack.append(toks[0])
        toks = toks[1:]
        for tok in toks:
            if tok in ("", "."):
                continue
            elif ".." ==  tok:
                if len(stack) > 0 and "" != stack[len(stack) - 1]:   # root / should not be poped to distinguish abs path and rel path
                    stack.pop()
                #else:
                #    return ""         # /home/../../..
            else:
                stack.append(tok)
        len_stack = len(stack)
        if len_stack >1:
            return "/".join(stack) if "" == stack[0] else "/" + "/".join(stack)
        elif (1 == len_stack and "" == stack[0]) or 0 == len_stack:
            return "/"
```
