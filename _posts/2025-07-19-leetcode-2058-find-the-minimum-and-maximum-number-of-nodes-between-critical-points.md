---
title: 2058. 找出临界点之间的最小和最大距离
date: 2025-07-19 19:15:00 +0800
categories: [Leetcode, LinkedList]
tags: [leetcode, linked-list]
author: ayou
description: 统计链表中极值节点之间距离的最大与最小距离。遍历并统计。
comments: true
---

## 原题
[2058. 找出临界点之间的最小和最大距离](https://leetcode.cn/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points/)

## 题解
**详情**：[一次遍历 + 常数空间](https://leetcode.cn/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points/solutions/1075991/go-mo-ni-bian-li-lian-biao-bian-li-lin-j-rx9s)

## 代码
```python
class Solution:
    def nodesBetweenCriticalPoints(self, head: Optional[ListNode]) -> List[int]:
        min_dist = max_dist = -1
        first = last = -1
        
        position = 0
        current = head
        while current.next.next:
            x, y, z = current.val, current.next.val, current.next.next.val
            if y > max(x, z) or y < min(x, z):
                if last != -1:
                    dist = position - last
                    if min_dist == -1:
                        min_dist = dist
                    else:
                        min_dist = min(min_dist, dist)

                    max_dist = position - first
                
                if first == -1:
                    first = position
                last = position            
            position += 1
            current = current.next
        
        return [min_dist, max_dist]
```
