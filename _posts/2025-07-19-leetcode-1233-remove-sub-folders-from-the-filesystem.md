---
title: 删除子文件夹
date: 2025-07-19 17:30:00 +0800
categories: [Leetcode, Sort]
tags: [leetcode, sort]
author: ayou
description: 删除为其他子文件夹的文件夹。排序后判定。
comments: true
---

## 原题
[1233. 删除子文件夹](https://leetcode.cn/problems/remove-sub-folders-from-the-filesystem/)

## 题解
**思路**：排序后，子文件夹的父文件夹一定在其左侧。
**详情**：[排序](https://leetcode.cn/problems/remove-sub-folders-from-the-filesystem/solutions/3727677/pai-xu-pythonjavaccgojsrust-by-endlessch-l0q2)

## 代码
```python
class Solution:
    def removeSubfolders(self, folder: List[str]) -> List[str]:
        folder.sort()
        answer = [folder[0]]
        for sub in folder[1:]:
            last = answer[-1]
            if not sub.startswith(last) or sub[len(last)] != '/':
                answer.append(sub)
        return answer
```
