---
title: 电话号码的字母组合
date: 2025-06-15 16:45:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, base, backtracking]
author: ayou
description: 求数字映射下的所有可能排列。夯实基础-回溯。
comments: true
---

## 原题
[17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/description/)

## 题解
**详情**：[【视频】回溯不会写？套路在此！（Python/Java/C++/Go/JS/Rust）](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/solutions/2059416/hui-su-bu-hui-xie-tao-lu-zai-ci-pythonja-3orv)

## 代码
```python
M = "", "", "abc", "def", "ghi", "jkl", "mno", "qprs", "tuv", "wxyz"

class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        n = len(digits)
        if n == 0:
            return []
        
        answer = []
        path = [''] * n

        def dfs(i):
            if i == n:
                answer.append(''.join(path))
                return
            for c in M[int(digits[i])]:
                path[i] = c
                dfs(i+1)

        dfs(0)
        return answer
```
{: file="dfs"}

```python
M = "", "", "abc", "def", "ghi", "jkl", "mno", "qprs", "tuv", "wxyz"

class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        n = len(digits)
        if n == 0:
            return []
        
        answer = []
        path = []

        def dfs(i):
            if i == n:
                answer.append(''.join(path))
                return
            for c in M[int(digits[i])]:
                path.append(c)
                dfs(i+1)
                path.pop()

        dfs(0)
        return answer
```
{: file="another dfs"}
