---
title: 2966. 划分数组并满足最大差限制
date: 2025-06-18 12:30:00 +0800
categories: [Leetcode, Greedy]
tags: [leetcode, greedy]
author: ayou
description: 划分数组为多个，要求子集差满足限制。贪心。
comments: true
---

## 原题
[2966. 划分数组并满足最大差限制](https://leetcode.cn/problems/divide-array-into-arrays-with-max-difference/description/)

## 题解
**详情**：[排序后切分（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/divide-array-into-arrays-with-max-difference/solutions/2569341/pai-xu-hou-qie-fen-pythonjavacgo-by-endl-lewc)

## 代码
```python
class Solution:
    def divideArray(self, nums: List[int], k: int) -> List[List[int]]:
        nums.sort()
        answer = []
        for i in range(0, len(nums), 3):
            if nums[i+2] - nums[i] > k:
                return []
            answer.append(nums[i:i+3])
        return answer
```
