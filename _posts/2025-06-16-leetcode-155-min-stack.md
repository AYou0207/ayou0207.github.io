---
title: 155. 最小栈
date: 2025-06-16 11:45:00 +0800
categories: [Leetcode, Stack]
tags: [leetcode, stack, custom-data-structure]
author: ayou
description: 构建栈，能在常数时间内检索到最小元素。数据结构构建-栈。
comments: true
---

## 原题
[155. 最小栈](https://leetcode.cn/problems/min-stack/description/)

## 题解
**详情**：[本质是维护前缀最小值，简洁写法！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/min-stack/solutions/2974438/ben-zhi-shi-wei-hu-qian-zhui-zui-xiao-zh-x0g8)

## 代码
```python
class MinStack:

    def __init__(self):
        self.stk = [(0, inf)]
        
    def push(self, val: int) -> None:
        self.stk.append(
            (val, min(self.stk[-1][1], val))
        )
        
    def pop(self) -> None:
        self.stk.pop()
        
    def top(self) -> int:
        return self.stk[-1][0]

    def getMin(self) -> int:
        return self.stk[-1][1]
```
