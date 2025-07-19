---
title: 416. 分割等和子集
date: 2025-06-22 20:45:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 判断数组是否可以划分为两个总和相等的子数组。01背包问题变体。
comments: true
---

## 原题
[416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/description/)

## 题解
**思路**：转化为数字的选取，目标值为总和的一半。目标为求是否存在可行方案。递推公式为：
$$
\text{dfs}(i, c) = \text{dfs}(i-1, c) | \text{dfs}(i-1, c-w_i)
$$

**详情**：[三种写法：记忆化搜索 / 递推 / bitset 优化](https://leetcode.cn/problems/partition-equal-subset-sum/solutions/2785266/0-1-bei-bao-cong-ji-yi-hua-sou-suo-dao-d-ev76)

## 代码
```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        @cache
        def dfs(i: int, c: int) -> bool:
            if i < 0:
                return c == 0
            return c >= nums[i] and dfs(i-1, c-nums[i]) or dfs(i-1, c)

        s = sum(nums)
        return s % 2 == 0 and dfs(len(nums) - 1, s // 2)
```
{: file="DFS"}

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        s = sum(nums)
        if s % 2:
            return False
        
        s //= 2
        n = len(nums)
        dp = [[False] * (s+1) for _ in range(n+1)]
        dp[0][0] = True
        for i, w in enumerate(nums):
            for c in range(s+1):
                dp[i+1][c] = dp[i][c] or c >= w and dp[i][c-w]
        return dp[n][s]
```
{: file="递推"}

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        s = sum(nums)
        if s % 2:
            return False
        
        s //= 2
        dp = [True] + [False] * s
        prefix = 0
        for w in nums:
            # prefix 为前缀和
            prefix += w
            # 子数组的和一定小于前缀和，因此可以从 min(prefix, s) 开始遍历
            for c in range(min(prefix, s), w-1, -1):
                dp[c] = dp[c] or dp[c-w]
            if dp[s]:
                return True
        return False
```
{: file="O(n)"}