---
title: 单词搜索
date: 2025-06-15 21:00:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, base, backtracking]
author: ayou
description: 求数组中是否存在一条路径能够构成指定单词。夯实基础-回溯 & 剪枝。
comments: true
---

## 原题
[79. 单词搜索](https://leetcode.cn/problems/word-search/description/)

## 题解
**详情**：[极致优化！代码击败接近 100%！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/word-search/solutions/2927294/liang-ge-you-hua-rang-dai-ma-ji-bai-jie-g3mmm)

## 代码
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        cnt = Counter(c for row in board for c in row)
        if not cnt >= Counter(word):
            return False
        if cnt[word[-1]] < cnt[word[0]]:
            word = word[::-1]
        
        m, n = len(board), len(board[0])

        def dfs(i: int, j: int, k: int) -> bool:
            if board[i][j] != word[k]:
                return False
            if k == len(word) - 1:
                return True
            
            # 标记 - 已访问
            board[i][j] = ''
            for x, y in (
                (i, j-1),
                (i, j+1),
                (i-1, j),
                (i+1, j)
            ):
                if 0 <= x < m and 0 <= y < n and dfs(x, y, k+1):
                    return True
            # 还原现场
            board[i][j] = word[k]
            return False
        
        return any(
            dfs(i, j, 0)
            for i in range(m)
            for j in range(n)
        )
```
