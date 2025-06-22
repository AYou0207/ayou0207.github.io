---
title: 目标和
date: 2025-06-22 21:10:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 数组中的每个元素可以保持原先值或取相反数，使得最终总和等于目标值。01背包问题变体。
comments: true
---

## 原题
[494. 目标和](https://leetcode.cn/problems/target-sum/description/)

## 题解
**思路**：转化为数字的选取，使得选取数字的总和为 原先数组总和与目标值的和的一半。求方案数。

**详情**：[两种方法：0-1 背包 / 折半枚举](https://leetcode.cn/problems/target-sum/solutions/2119041/jiao-ni-yi-bu-bu-si-kao-dong-tai-gui-hua-s1cx)

## 代码
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        capacity = sum(nums) - abs(target)
        if capacity < 0 or capacity % 2:
            return 0
        capacity //= 2

        @cache
        def dfs(i: int, c: int) -> int:
            if i < 0:
                return 1 if c == 0 else 0
            if c < nums[i]:
                return dfs(i-1, c)
            return dfs(i-1, c) + dfs(i-1, c-nums[i])
        
        return dfs(len(nums)-1, capacity)
```
{: file="DFS"}

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        capacity = sum(nums) - abs(target)
        if capacity < 0 or capacity % 2:
            return 0
        capacity //= 2

        n = len(nums)
        dp = [[0] * (capacity+1) for _ in range(n+1)]
        dp[0][0] = 1
        for i, w in enumerate(nums):
            for c in range(capacity+1):
                if c < w:
                    dp[i+1][c] = dp[i][c]
                else:
                    dp[i+1][c] = dp[i][c] + dp[i][c-w]

        return dp[n][capacity]
```
{: file="递推"}

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        capacity = sum(nums) - abs(target)
        if capacity < 0 or capacity % 2:
            return 0
        capacity //= 2

        n = len(nums)
        dp = [[0] * (capacity+1) for _ in range(2)]
        dp[0][0] = 1
        for i, w in enumerate(nums):
            for c in range(capacity+1):
                if c < w:
                    dp[(i+1)%2][c] = dp[i%2][c]
                else:
                    dp[(i+1)%2][c] = dp[i%2][c] + dp[i%2][c-w]

        return dp[n%2][capacity]
```
{: file="滚动数组"}

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        capacity = sum(nums) - abs(target)
        if capacity < 0 or capacity % 2:
            return 0
        capacity //= 2

        n = len(nums)
        dp = [1] + [0] * capacity
        for w in nums:
            for c in range(capacity, w-1, -1):
                dp[c] = dp[c] + dp[c-w]

        return dp[capacity]
```
{: file="一个数组"}