---
title: 3489. 零数组变换 IV
date: 2025-06-24 13:00:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 判断一定范围内的数字是否存在等于目标值的，返回这些位置的索引序列。滑动窗口。
comments: true
---

## 原题
[3489. 零数组变换 IV](https://leetcode.cn/problems/zero-array-transformation-iv/description/)

## 题解
**01背包思路**：转换为多个 01背包问题：每个非零位置都相当于一个背包；每个`query`都相当于一个物品。目标就是求是否存在可行解。

**详情**：[两种方法：0-1 背包 / 二分答案+多重背包](https://leetcode.cn/problems/zero-array-transformation-iv/solutions/3613907/0-1-bei-bao-pythonjavacgo-by-endlesschen-2y0l)

## 代码
### 01背包
```python
class Solution:
    def minZeroArray(self, nums: List[int], queries: List[List[int]]) -> int:
        answer = 0
        for i, num in enumerate(nums):
            if num == 0:
                continue
            dp = [True] + [False] * num
            for k, (l, r, weight) in enumerate(queries):
                if not l <= i <= r:
                    continue
                for capacity in range(num, weight-1, -1):
                    dp[capacity] = dp[capacity] or dp[capacity - weight]
                if dp[num]:
                    answer = max(answer, k+1)
                    break
            else:
                return -1
        return answer
```

复杂度优化 - bitset 技巧
```python
class Solution:
    def minZeroArray(self, nums: List[int], queries: List[List[int]]) -> int:
        answer = 0
        for i, num in enumerate(nums):
            if num == 0:
                continue
            dp = 1
            for k, (l, r, weight) in enumerate(queries, start=1):
                if not l <= i <= r:
                    continue
                dp |= dp << weight
                if dp >> num & 1:
                    answer = max(answer, k)
                    break
            else:
                return -1
        return answer
```
