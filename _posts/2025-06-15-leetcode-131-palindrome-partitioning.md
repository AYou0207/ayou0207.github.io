---
title: 分割回文串
date: 2025-06-15 21:25:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, base, backtracking]
author: ayou
description: 求字符串分割后所有子串均为回文的组合可能。夯实基础-回溯。
comments: true
---

## 原题
[131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/description/)

## 题解
**思路**：回溯；`dfs`中需要跟踪两个状态 - `i` 当前字符位置 & `start` 当前回文串开始的位置。

**详情**：[【视频】回溯不会写？套路在此！（Python/Java/C++/Go/JS）](https://leetcode.cn/problems/palindrome-partitioning/solutions/2059414/hui-su-bu-hui-xie-tao-lu-zai-ci-pythonja-fues)

## 代码
```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        n = len(s)

        answer = []
        path = []

        # 考虑 i 后的字符串如何选择
        # start 表示当前这段回文子串的开始位置
        def dfs(i: int, start: int):
            if i == n:
                answer.append(path[:])
                return
            
            if i < n-1:
                dfs(i+1, start)

            t = s[start: i+1]
            if t == t[::-1]:
                path.append(t)
                dfs(i+1, i+1)
                path.pop()

        dfs(0, 0)
        return answer
```
