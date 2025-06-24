---
title: 找出数组中的所有 K 近邻下标
date: 2025-06-24 12:30:00 +0800
categories: [Leetcode, Slice]
tags: [leetcode, slice]
author: ayou
description: 判断一定范围内的数字是否存在等于目标值的，返回这些位置的索引序列。滑动窗口。
comments: true
---

## 原题
[2200. 找出数组中的所有 K 近邻下标](https://leetcode.cn/problems/find-all-k-distant-indices-in-an-array/description/)

## 题解
**详情**：[O(n) 做法](https://leetcode.cn/problems/find-all-k-distant-indices-in-an-array/solutions/1332985/mo-ni-by-endlesscheng-57j9)

## 代码
```python
class Solution:
    def findKDistantIndices(self, nums: List[int], key: int, k: int) -> List[int]:
        last = -inf
        for i in range(k-1, -1, -1):
            if nums[i] == key:
                last = i
                break
        
        answer = []
        n = len(nums)
        for i in range(n):
            if i + k < n and nums[i+k] == key:
                last = i + k
            if last >= i - k:
                answer.append(i)
        return answer
```
