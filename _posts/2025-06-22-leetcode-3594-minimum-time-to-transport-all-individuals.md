---
title: 3594. 所有人渡河所需的最短时间
date: 2025-06-22 14:55:00 +0800
categories: [Leetcode, Dijkstra]
tags: [leetcode, graph, hard, Dijkstra]
author: ayou
description: 增加节点成本使得所有根到叶子的路径和相等。DFS-图中路径和的计算。
comments: true
---

## 原题
[3594. 所有人渡河所需的最短时间](https://leetcode.cn/problems/minimum-time-to-transport-all-individuals/description/)

## 题解
**详情**：[子集状压 + Dijkstra](https://leetcode.cn/problems/minimum-time-to-transport-all-individuals/solutions/3705712/zi-ji-zhuang-ya-dijkstrapythonjavacgo-by-hkla)

## 代码
```python
class Solution:
    def minTime(self, n: int, k: int, m: int, times: List[int], mul: List[float]) -> float:
        u = 1 << n

        # 预处理每个 time 子集的最大值
        max_time = [0] * u
        for i, time in enumerate(times):
            high = 1 << i
            for sub in range(high):
                max_time[high | sub] = max(max_time[sub], time)
        

        # 预处理每个集合的大小 <= k 的非空子集
        sub_masks = [[] for _ in range(u)]
        for i in range(u):
            sub = i
            while sub:
                if sub.bit_count() <= k:
                    sub_masks[i].append(sub)
                sub = (sub - 1) & i

        distance = [[inf] * u for _ in range(m)]
        h = []

        def push(d: float, stage: int, mask: int):
            if d < distance[stage][mask]:
                distance[stage][mask] = d
                heappush(h, (d, stage, mask))
        
        push(0, 0, u-1)

        while h:
            d, stage, remain = heappop(h)
            if remain == 0:
                return d
            if d > distance[stage][remain]:
                continue
            for sub in sub_masks[remain]:
                cost = max_time[sub] * mul[stage]
                cur_stage = (stage + floor(cost)) % m
                # 所有人都过河了
                if sub == remain:
                    push(d + cost, cur_stage, 0)
                else:
                    # 枚举回来的人（可以是之前过河的人）
                    s = (u - 1) ^ remain ^ sub
                    while s:
                        lowbit = s & -s
                        return_time = max_time[lowbit] * mul[cur_stage]
                        push(d + cost + return_time, (cur_stage + floor(return_time)) % m, remain ^ sub ^ lowbit)
                        s ^= lowbit
        
        return -1
```
