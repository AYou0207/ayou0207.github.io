---
title: 46. 全排列
date: 2025-06-15 16:40:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, base, backtracking]
author: ayou
description: 求数组的所有可能排列。夯实基础-回溯。
comments: true
---

## 原题
[46. 全排列](https://leetcode.cn/problems/permutations/description/)

## 题解
**详情**：[全排列](https://leetcode.cn/problems/permutations/solutions/218275/quan-pai-lie-by-leetcode-solution-2)

## 代码
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        answer = []
        path = []

        def dfs(i):
            if i == n:
                answer.append(path[:])
                return
            
            for num in nums:
                if num not in path:
                    path.append(num)
                    dfs(i+1)
                    path.pop()
        
        dfs(0)
        return answer
```
{: file="dfs"}
