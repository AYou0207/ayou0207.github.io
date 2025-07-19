---
title: 3592. 硬币面值还原
date: 2025-06-22 14:45:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 给出硬币组合方案个数，求基础硬币面值。完全背包问题-逆问题。
comments: true
---

## 原题
[3592. 硬币面值还原](https://leetcode.cn/problems/inverse-coin-change/description/)

## 题解
**详情**：[完全背包](https://leetcode.cn/problems/inverse-coin-change/solutions/3705647/wan-quan-bei-bao-pythonjavacgo-by-endles-y6oq)

## 代码
```python
class Solution:
    def minIncrease(self, n: int, edges: List[List[int]], cost: List[int]) -> int:
        graph = [[] for _ in range(n)]
        for u, v in edges:
            graph[u].append(v)
            graph[v].append(u)

        answer = 0
        def dfs(u: int, father: int, path: int) -> int:
            path += cost[u]
            vs = graph[u]
            if len(vs) == 1:
                return path
            
            mv = 0
            cnt = 0
            for v in vs:
                if v == father:
                    continue
                
                child = dfs(v, u, path)
                if child > mv:
                    mv = child
                    cnt = 1
                elif child == mv:
                    cnt += 1
            
            nonlocal answer
            answer += len(vs) - 1 - cnt
            return mv

        # 避免误把根节点当作叶子
        graph[0].append(-1)
        dfs(0, -1, 0)
        return answer
```
