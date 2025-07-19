---
title: 3585. 树中找到带权中位节点
date: 2025-06-15 15:45:00 +0800
categories: [Leetcode, LCA]
tags: [leetcode, hard, LCA]
author: ayou
description: 求树中两个节点的权值中位节点。LCA（最近祖先）变体。
comments: true
---

## 原题
[3585. 树中找到带权中位节点](https://leetcode.cn/problems/find-weighted-median-node-in-tree/description/)

## 题解
**详情**：[【模板】最近公共祖先 LCA（Python/Java/C++/Go）](https://leetcode.cn/problems/find-weighted-median-node-in-tree/solutions/3700556/mo-ban-zui-jin-gong-gong-zu-xian-lcapyth-6ekj)

## 代码
```python
class LCA:
    def __init__(self, edges: list[list[int]]):
        n = len(edges) + 1
        self.m = m = n.bit_length()
        graph = [[] for _ in range(n)]
        for u, v, w in edges:
            graph[u].append((v, w))
            graph[v].append((u, w))
        
        depth = [0] * n
        distance = [0] * n
        parent = [[-1] * m for _ in range(n)]
        
        def dfs(u: int, father: int):
            parent[u][0] = father
            for v, w in graph[u]:
                if v != father:
                    depth[u] = depth[v] + 1
                    distance[v] = distance[u] + weight
                    dfs(v, u)
        
        dfs(0, -1)

        for i in range(m-1):
            for u in range(n):
                if (p := parent[u][i]) != -1:
                    parent[u][i+1] = parent[p][i]
        
        self.depth = depth
        self.distance = distance
        self.parent = parent
    
    def get_kth_ancestor(self, node: int, k: int) -> int:
        for i in range(k.bit_length()):
            if k >> i & 1:
                node = self.parent[node][i]
        return node

    
    def get_lca(self, u: int, v: int) -> int:
        if u == v:
            return u
        if self.depth[v] > self.depth[u]:
            u, v = v, u
        v = self.get_kth_ancestor(u, self.depth[v] - self.depth[u])
        for i in range(self.m-1, -1, -1):
            pu, pv = self.parent[u][i], self.parent[v][i]
            if pu != pv:
                u, v = pu, pv
        return self.parent[u][0]
    
    def get_distance(self, u: int, v: int) -> int:
        return self.distance[u] + self.distance[v] - self.distance[
            self.get_lca(u, v)
        ] * 2
    
    # 从 u 往上跳【至多】d 距离，返回最远能到达的节点
    def upto_distance(self, u: int, d: int) -> int:
        du = self.distance[u]
        for i in range(self.m-1, -1, -1):
            parent = self.parent[u][i]
            if parent != -1 and du - self.distance[parent] <= d:
                u = parent
        return u


class Solution:
    def findMedian(self, n: int, edges: list[list[int]], queries: list[list[int]]) -> list[int]:
        graph = LCA(edges)
        answer = []
        for u, v in queries:
            if u == v:
                answer.append(u)
                continue
            lca = graph.get_lca(u, v)
            distance = graph.distance[u] + graph.distance[v] - graph.distance[lca] * 2
            half = (distance + 1) // 2
            if graph.distance[u] - graph.distance[lca] >= half:
                to = graph.upto_distance(u, half - 1)
                current = graph.parent[to][0]
            else:
                current = graph.upto_distance(v, distance - half)
            answer.append(current)
        return answer
```
