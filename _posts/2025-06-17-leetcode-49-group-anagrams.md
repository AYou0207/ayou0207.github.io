---
title: 字母异位词分组
date: 2025-06-17 13:15:00 +0800
categories: [Leetcode, Hash]
tags: [leetcode, hash, easy]
author: ayou
description: 记录每个位置的左右小于当前高度的位置。单调栈。
comments: true
---

## 原题
[49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/description/)

## 题解
**详情**：[哈希表分组，简洁写法（Python/Java/C++/Go/JS/Rust）](https://leetcode.cn/problems/group-anagrams/solutions/2718519/ha-xi-biao-fen-zu-jian-ji-xie-fa-pythonj-1ukv)

## 代码
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dct = defaultdict(list)
        for s in strs:
            dct[''.join(sorted(s))].append(s)
        return list(dct.values())
```
