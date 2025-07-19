---
title: 22. 括号生成
date: 2025-06-15 17:10:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, backtracking, medium]
author: ayou
description: 生成所有的合法括号字符串。回溯。
comments: true
---

## 原题
[22. 括号生成](https://leetcode.cn/problems/generate-parentheses/description/)

## 题解
**思路**：回溯。同时注意除了枚举括号个数 `i` 之外，还需要枚举当前是否可以插入左括号 或 右括号。

**详情**：[回溯不会写？套路在此！（Python/Java/C++/Go/JS）](https://leetcode.cn/problems/generate-parentheses/solutions/2071015/hui-su-bu-hui-xie-tao-lu-zai-ci-pythonja-wcdw)

## 代码
```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        m = n * 2
        answer = []
        path = []

        def dfs(i: int, left: int):
            if i == m:
                answer.append(''.join(path))
                return
            
            if left < n:
                path.append('(')
                dfs(i+1, left+1)
                path.pop()
            
            if i - left < left:
                path.append(')')
                dfs(i+1, left)
                path.pop()
        
        dfs(0, 0)
        return answer
```
