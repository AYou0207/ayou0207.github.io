---
title: 2181. 合并零之间的节点
date: 2025-07-19 19:20:00 +0800
categories: [Leetcode, LinkedList]
tags: [leetcode, linked-list]
author: ayou
description: 加和链表中非零节点的和，并以链表的形式返回。遍历链表并统计。
comments: true
---

## 原题
[2181. 合并零之间的节点](https://leetcode.cn/problems/merge-nodes-in-between-zeros/)

## 题解
**详情**：[原地做法，O(1) 空间](https://leetcode.cn/problems/merge-nodes-in-between-zeros/solutions/1278727/jian-ji-xie-fa-by-endlesscheng-c4gf)

## 代码
```python
class Solution:
    def mergeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        node = head.next
        val = 0
        while node is not None:
            if node.val > 0:
                val += node.val
            else:
                current.next.val = val

                current = current.next
                val = 0
            node = node.next
        current.next = None
        return head.next
```
