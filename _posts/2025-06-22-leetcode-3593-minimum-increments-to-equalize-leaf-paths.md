---
title: 使叶子路径成本相等的最小增量
date: 2025-06-22 14:35:00 +0800
categories: [Leetcode, GraphDFS]
tags: [leetcode, graph, dfs]
author: ayou
description: 增加节点成本使得所有根到叶子的路径和相等。DFS-图中路径和的计算。
comments: true
---

## 原题
[3593. 使叶子路径成本相等的最小增量](https://leetcode.cn/problems/minimum-increments-to-equalize-leaf-paths/description/)

## 题解
**详情**：[统计最大路径和的出现次数](https://leetcode.cn/problems/minimum-increments-to-equalize-leaf-paths/solutions/3705650/tong-ji-zui-da-lu-jing-he-de-chu-xian-ci-bh9f)

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
