---
title: 3583. 统计特殊三元组
date: 2025-06-15 14:20:00 +0800
categories: [Leetcode, Prefix]
tags: [leetcode, prefix, medium]
author: ayou
description: 求数组中三元组个数（第一个&第三个均为第二个的两倍）。枚举中间数，前后缀缓存。
comments: true
---

## 原题
[3583. 统计特殊三元组](https://leetcode.cn/problems/count-special-triplets/description/)

## 题解
**思路**：枚举中间数，前后缀缓存。

**详情**：[枚举中间 + 前后缀分解（Python/Java/C++/Go）](https://leetcode.cn/problems/count-special-triplets/solutions/3700554/mei-ju-zhong-jian-qian-hou-zhui-fen-jie-5uad8)

## 代码
```python
class Solution:
    def specialTriplets(self, nums: List[int]) -> int:
        MOD = 1_000_000_007
        suffix = Counter(nums)

        answer = 0
        prefix = defaultdict(int)

        for num in nums:
            suffix[num] -= 1
            answer += prefix[num * 2] * suffix[num * 2]
            prefix[num] += 1
        
        return answer % MOD
```
