---
title: 2915. 和为目标值的最长子序列的长度
date: 2025-06-22 21:30:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 取数组中的子序列使得和等于目标值，求这种子序列的最长长度。01背包问题变体。
comments: true
---

## 原题
[2915. 和为目标值的最长子序列的长度](https://leetcode.cn/problems/length-of-the-longest-subsequence-that-sums-to-target/description/)

## 题解
**思路**：转化为数字的选取，使得选取数字的总和为目标值。求物体的最大数目。

**详情**：[两种方法：0-1 背包 / 折半枚举](https://leetcode.cn/problems/length-of-the-longest-subsequence-that-sums-to-target/solutions/2502839/mo-ban-qia-hao-zhuang-man-xing-0-1-bei-b-0nca)

## 代码
```python
class Solution:
    def lengthOfLongestSubsequence(self, nums: List[int], target: int) -> int:
        @cache
        def dfs(i: int, c: int):
            if i < 0:
                return 0 if c == 0 else -inf
            if c < nums[i]:
                return dfs(i-1, c)
            return max(
                dfs(i-1, c),
                dfs(i-1, c-nums[i]) + 1
            )
        answer = dfs(len(nums)-1, target)
        # 防止爆内存
        dfs.cache_clear()
        return answer if answer > 0 else -1
```
{: file="DFS"}

```python
class Solution:
    def lengthOfLongestSubsequence(self, nums: List[int], target: int) -> int:
        n = len(nums)
        dp = [[-inf] * (target+1) for _ in range(n+1)]
        dp[0][0] = 0
        for i, w in enumerate(nums):
            for c in range(target+1):
                if c < w:
                    dp[i+1][c] = dp[i][c]
                else:
                    dp[i+1][c] = max(dp[i][c], dp[i][c-w]+1)
        return dp[n][target] if dp[n][target] > 0 else -1
```
{: file="递推"}

```python
class Solution:
    def lengthOfLongestSubsequence(self, nums: List[int], target: int) -> int:
        dp = [0] + [-inf] * target
        prefix = 0
        for w in nums:
            # 记录前缀和
            prefix += w
            # 优化点：min(prefix, target)
            # 只需要枚举到 前缀和 即可
            for c in range(min(prefix, target), w-1, -1):
                dp[c] = max(dp[c], dp[c-w]+1)
        return dp[target] if dp[target] > 0 else -1
```
{: file="一个数组"}