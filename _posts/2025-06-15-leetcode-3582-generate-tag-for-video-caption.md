---
title: 为视频标题生成标签
date: 2025-06-15 14:20:00 +0800
categories: [Leetcode, Simulation]
tags: [leetcode, simulation, easy]
author: ayou
description: 按要求对字符串进行转换。模拟即可。
comments: true
---

## 原题
[3582. 为视频标题生成标签](https://leetcode.cn/problems/generate-tag-for-video-caption/description/)

## 题解
**思路**：模拟

**详情**：另一种思路，用库函数实现：
[库函数模拟（Python/Java/C++/Go）](https://leetcode.cn/problems/generate-tag-for-video-caption/solutions/3700564/ku-han-shu-mo-ni-pythonjavacgo-by-endles-glg4)

## 代码
```python
class Solution:
    def generateTag(self, s: str) -> str:
        caption = '#'
        num = 1
        first_char = False
        n = len(s)
        start = 0
        while start < n and s[start] == ' ':
            start += 1
        for index in range(start, n):
            ch = s[index]
            if ch == ' ':
                first_char = True
            else:
                if first_char:
                    ch = ch.upper()
                else:
                    ch = ch.lower()
                first_char = False
                caption += ch
                num += 1
                if num >= 100:
                    break
        
        return caption
```
