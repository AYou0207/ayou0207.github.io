---
title: 51. N 皇后
date: 2025-06-15 21:30:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, medium, backtracking]
author: ayou
description: 构造 n 皇后的所有解决方案。夯实基础-回溯。
comments: true
---

## 原题
[51. N 皇后](https://leetcode.cn/problems/n-queens/description/)

## 题解
**思路**：回溯；n 皇后问题中为了防止对角线冲突，有一个技巧：正对角线 `r+c` & 负对角线 `r-c`。

**详情**：[【视频讲解】排列型回溯，简洁高效！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/n-queens/solutions/2079586/hui-su-tao-lu-miao-sha-nhuang-hou-shi-pi-mljv)

## 代码
```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        answer = []

        queens = [0] * n
        col = [False] * n
        diag1 = [False] * (n*2-1)
        diag2 = [False] * (n*2-1)

        def dfs(r: int):
            if r == n:
                answer.append([
                    '.' * c + 'Q' + '.' * (n-1-c)
                    for c in queens
                ])
                return
            
            for c, ok in enumerate(col):
                if not ok and not diag1[r+c] and not diag2[r-c]:
                    queens[r] = c
                    col[c] = diag1[r+c] = diag2[r-c] = True
                    dfs(r+1)
                    col[c] = diag1[r+c] = diag2[r-c] = False
        
        dfs(0)
        return answer
```
