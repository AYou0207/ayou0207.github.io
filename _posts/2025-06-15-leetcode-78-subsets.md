---
title: 子集
date: 2025-06-15 16:25:00 +0800
categories: [Leetcode, Backtracking]
tags: [leetcode, base, backtracking]
author: ayou
description: 求数组的所有可能子集。夯实基础-回溯。
comments: true
---

## 原题
[78. 子集](https://leetcode.cn/problems/subsets/description/)

## 题解
**详情**：[【视频】三种写法：选或不选/枚举选哪个/二进制枚举（Python/Java/C++/Go/JS/Rust）](https://leetcode.cn/problems/subsets/solutions/2059409/hui-su-bu-hui-xie-tao-lu-zai-ci-pythonja-8tkl)

## 代码
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        answer = []
        path = []
        n = len(nums)

        def dfs(i: int):
            if i == n:
                answer.append(path[:])
                return
            
            # 不选 nums[i]
            dfs(i+1)
            # 选 nums[i]
            path.append(nums[i])
            dfs(i+1)
            path.pop()
        
        dfs(0)
        return answer
```
{: file="dfs"}

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        return [
            [
                x for j, x in enumerate(nums) if (i >> j) & 1
            ]
            for i in range(1 << len(nums))
        ]
```
{: file="bitset" }
