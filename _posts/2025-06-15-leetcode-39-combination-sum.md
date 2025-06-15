---
title: 组合总和
date: 2025-06-15 16:55:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, backtracking, medium]
author: ayou
description: 求数组下组合为目标值的所有集合。回溯。
comments: true
---

## 原题
[39. 组合总和](https://leetcode.cn/problems/combination-sum/description/)

## 题解
**详情**：[三种方法：选或不选/枚举选哪个/完全背包预处理+可行性剪枝（Python/Java/C++/Go）](https://leetcode.cn/problems/combination-sum/solutions/2747858/liang-chong-fang-fa-xuan-huo-bu-xuan-mei-mhf9)

## 代码
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        answer = []
        path = []

        def dfs(i: int, remain: int):
            if remain == 0:
                answer.append(path[:])
                return
            
            if remain < candidates[i]:
                return
            
            for j in range(i, len(candidates)):
                path.append(candidates[j])
                dfs(j, remain - candidates[j])
                path.pop()
        
        dfs(0, target)
        return answer
```
