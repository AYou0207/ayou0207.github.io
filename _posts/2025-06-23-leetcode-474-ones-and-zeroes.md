---
title: 474. 一和零
date: 2025-06-23 22:05:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 找出 k 进制下的回文数，枚举+回文数判断即可。
comments: true
---

## 原题
[474. 一和零](https://leetcode.cn/problems/ones-and-zeroes/description/)

## 题解
**详情**：[一步步思考：从记忆化搜索到递推到空间优化！](https://leetcode.cn/problems/ones-and-zeroes/solutions/3038333/yi-bu-bu-si-kao-cong-ji-yi-hua-sou-suo-d-lqio)

## 代码
```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        cnt0, cnt1 = [], []
        for s in strs:
            _0, _1 = 0, 0
            for ch in s:
                if ch == '0':
                    _0 += 1
                else:
                    _1 += 1
            cnt0.append(_0)
            cnt1.append(_1)
        
        @cache
        def dfs(i: int, c0: int, c1: int) -> int:
            if i < 0:
                return 0
            answer = dfs(i-1, c0, c1)
            if c0 >= cnt0[i] and c1 >= cnt1[i]:
                answer = max(
                    answer,
                    dfs(i-1, c0-cnt0[i], c1-cnt1[i]) + 1
                )
            return answer
        
        return dfs(len(strs)-1, m, n)
```
