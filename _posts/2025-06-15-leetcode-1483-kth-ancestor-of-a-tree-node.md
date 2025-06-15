---
title: 树节点的第 K 个祖先
date: 2025-06-15 15:25:00 +0800
categories: [Leetcode, Template, LCA]
tags: [leetcode, LCA, template]
author: ayou
description: 求树上的第 K 个祖先。模板题 - 树上倍增算法
comments: true
---

## 原题
[1483. 树节点的第 K 个祖先](https://leetcode.cn/problems/kth-ancestor-of-a-tree-node/description/)

## 题解
**详情**：[【模板讲解】树上倍增算法（以及最近公共祖先）Python/Java/C++/Go](https://leetcode.cn/problems/kth-ancestor-of-a-tree-node/solutions/2305895/mo-ban-jiang-jie-shu-shang-bei-zeng-suan-v3rw)

## 代码
```python
class TreeAncestor:

    def __init__(self, n: int, parent: list[int]):
        m = n.bit_length() - 1
        parent = [
            [p] + [-1] * m for p in parent
        ]
        for i in range(m):
            for x in range(n):
                if (p := parent[x][i]) != -1:
                    parent[x][i+1] = parent[p][i]
        self.parent = parent
    
    def getKthAncestor(self, node: int, k: int) -> int:
        for i in range(k.bit_length()):
            # k 的二进制从低到高第 i 位是 1
            if k >> i & 1:
                node = self.parent[node][i]
                if node < 0:
                    break
        return node

    def getKthAncestor_lowbit(self, node: int, k: int) -> int:
        # 另一种写法, 不断去掉 k 的最低位的 1
        while k and node != -1:
            lowbit = k & -k
            node = self.parent[node][lowbit.bit_length() - 1]
            k ^= lowbit
        return node
```

## LCA 模板
```python
class TreeAncestor:
    def __init__(self, edges: list[list[int]]):
        n = len(edges) + 1
        m = n.bit_length()
        graph = [[] for _ in range(n)]
        for u, v in edges:
            g[u].append(v)
            g[v].append(u)
        
        depth = [0] * n
        parent = [[-1] * m for _ in range(n)]

        def dfs(u: int, father: int):
            parent[u][0] = father
            for v in g[u]:
                if v != father:
                    depth[v] = depth[u] + 1
                    dfs(v, x)
        
        dfs(0, -1)

        for i in range(m-1):
            for u in range(n):
                if (p := parent[u][i]) != -1:
                    parent[u][i+1] = parent[p][i]
        self.depth = depth
        self.parent = parent
    
    def get_kth_ancestor(self, node: int, k: int) -> int:
        for i in range(k.bit_length()):
            if k >> i & 1:
                node = self.parent[node][i]
        return node
    
    def get_lca(self, x: int, y: int) -> int:
        if self.depth[x] > self.depth[y]:
            x, y = y, x
        y = self.get_kth_ancestor(y, self.depth[y] - self.depth[x])
        if y == x:
            return x
        
        for i in range(len(self.parent[x]) - 1, -1, -1):
            px, py = self.parent[x][i], self.parent[y][i]
            if px != py:
                x, y = px, py
        return self.parent[x][0]
```