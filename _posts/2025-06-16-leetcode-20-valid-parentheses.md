---
title: 20. 有效的括号
date: 2025-06-16 11:40:00 +0800
categories: [Leetcode, Stack]
tags: [leetcode, stack, base]
author: ayou
description: 判断字符串的括号是否合法。夯实基础-栈。
comments: true
---

## 原题
[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/description/)

## 题解
**详情**：[括号消消乐：三种利用栈的写法，附题单！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/valid-parentheses/solutions/2809539/gua-hao-xiao-xiao-le-san-chong-li-yong-z-2xb3)

## 代码
```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2:
            return False
        m = {
            ")": "(",
            "]": "[",
            "}": "{"
        }
        stk = []
        for ch in s:
            if ch not in m:
                stk.append(ch)
            elif not stk or stk.pop() != m[ch]:
                return False
        return not stk
```
