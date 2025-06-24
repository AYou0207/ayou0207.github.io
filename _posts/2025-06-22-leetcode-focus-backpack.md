---
title: 动态规划 - 0-1 背包 及 完全背包
date: 2025-06-22 20:10:00 +0800
categories: [Leetcode, Focus]
tags: [leetcode, focus, backpack]
author: ayou
description: 背包问题集合。
math: true
comments: true
---

## 0-1 背包
**问题**：有$n$个物体，第$i$个物品的体积为$w_i$，价值为$v_i$。每个物品至多选一个，求体积和不超过$c$的最大价值和。

**求解思路**：回溯三问

1. 当前操作？枚举第$i$个物品选或不选：不选，剩余容量不变；选，剩余容量减少 $w_i$ —— 因此，状态转移为二元组：（第$i$个物品，剩余容量$c$）
2. 子问题？在剩余容量为$c$时，从前$i$个物品中得到的最大价值和
3. 状态转移？不选：在剩余容量为$c$时，从前$i-1$个物品中得到的最大价值和；选：在剩余容量为$c-w_i$时，从前$i-1$个物品中得到的最大价值和

总结，状态转移方程为：
$$
\text{dfs}(i, c) = \max(
    \text{dfs}(i-1, c),
    \text{dfs}(i-1, c-w_i) + v_i
)
$$

**参考实现**：
```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> int:

    @cache
    def dfs(i: int, c: int) -> int:
        if i < 0:
            return 0
        if c < weights[i]:
            return dfs(i-1, c)
        return max(
            dfs(i-1, c),
            dfs(i-1, c-weights[i]) + values[i]
        )

    return dfs(len(weights)-1, capacity)
```
{: file="0-1 Backpack" }

### 题目清单

- [416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/description/)
- [494. 目标和](https://leetcode.cn/problems/target-sum/description/)
- [2915. 和为目标值的最长子序列的长度](https://leetcode.cn/problems/length-of-the-longest-subsequence-that-sums-to-target/description/)
- [2787. 将一个数字表示成幂的和的方案数](https://leetcode.cn/problems/ways-to-express-an-integer-as-sum-of-powers/description/)
- [3180. 执行操作可获得的最大总奖励 I](https://leetcode.cn/problems/maximum-total-reward-using-operations-i/description/)
- [474. 一和零](https://leetcode.cn/problems/ones-and-zeroes/description/)
- [3489. 零数组变换 IV](https://leetcode.cn/problems/zero-array-transformation-iv/description/)
- [1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii/description/)
- [1774. 最接近目标价格的甜点成本](https://leetcode.cn/problems/closest-dessert-cost/description/)
- [879. 盈利计划](https://leetcode.cn/problems/profitable-schemes/description/)
- [3082. 求出所有子序列的能量和](https://leetcode.cn/problems/find-the-sum-of-the-power-of-all-subsequences/description/)
- [956. 最高的广告牌](https://leetcode.cn/problems/tallest-billboard/description/)
- [2518. 好分区的数目](https://leetcode.cn/problems/number-of-great-partitions/description/)
- [2742. 给墙壁刷油漆](https://leetcode.cn/problems/painting-the-walls/description/)
- [3287. 求出数组中最大序列值](https://leetcode.cn/problems/find-the-maximum-sequence-value-of-array/description/)
- [LCP 47. 入场安检](https://leetcode.cn/problems/oPs9Bm/description/)

## 完全背包
**问题**：有$n$种物体，第$i$个物品的体积为$w_i$，价值为$v_i$。每种物品可以重复选择，求体积和不超过$c$的最大价值和。

**求解思路**：回溯三问

1. 当前操作？枚举第$i$种物品选一个或不选：不选，剩余容量不变；选，剩余容量减少 $w_i$ —— 因此，状态转移为二元组：（第$i$个物品，剩余容量$c$）
2. 子问题？在剩余容量为$c$时，从前$i$种物品中得到的最大价值和
3. 状态转移？不选：在剩余容量为$c$时，从前$i-1$种物品中得到的最大价值和；选一个：在剩余容量为$c-w_i$时，从**前$i$种**物品中得到的最大价值和

总结，状态转移方程为：
$$
\text{dfs}(i, c) = \max(
    \text{dfs}(i-1, c),
    \text{dfs}({\color{\red} i}, c-w_i) + v_i
)
$$

**参考实现**：
```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> int:

    @cache
    def dfs(i: int, c: int) -> int:
        if i < 0:
            return 0
        if c < weights[i]:
            return dfs(i-1, c)
        return max(
            dfs(i-1, c),
            dfs(i, c-weights[i]) + values[i]
        )

    return dfs(len(weights)-1, capacity)
```
{: file="Total Backpack" }

### 题目清单

- [322. 零钱兑换](https://leetcode.cn/problems/coin-change/description/)
- [518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-ii/description/)
- [279. 完全平方数](https://leetcode.cn/problems/perfect-squares/description/)
- [1449. 数位成本和为目标值的最大数字](https://leetcode.cn/problems/form-largest-integer-with-digits-that-add-up-to-target/description/)

## 变体 & 空间复杂度优化

### 常见变体
以**0-1 背包**问题为例，有以下常见变种：
- 体积至多为`capacity`，求*方案数*或*最大价值和*或*是否可行*
- 体积恰好为`capacity`，求*方案数*或*最大价值和*或*最小价值和*或*是否可行*
- 体积至少为`capacity`，求*方案数*或*最小价值和*或*是否可行*

当目标为*最大价值数*时，递推公式，即
$$
\text{dfs}(i, c) = \max(
    \text{dfs}(i-1, c),
    \text{dfs}(i-1, c-w_i) + v_i
)
$$

求*方案数*时，递推公式中的 `\max` 需要替换为 `+`，即
$$
\text{dfs}(i, c) = \text{dfs}(i-1, c) + \text{dfs}(i-1, c-w_i)
$$

求*最小价值数*时，递推公式中的 `\max` 需要替换为 `\min`，即
$$
\text{dfs}(i, c) = \min(
    \text{dfs}(i-1, c),
    \text{dfs}(i-1, c-w_i) + v_i
)
$$

求*是否可行*时，递推公式中的 `\max` 需要替换为 `or` （布尔或操作），即
$$
\text{dfs}(i, c) = 
    \text{dfs}(i-1, c) \lor \text{dfs}(i-1, c-w_i)
$$

而体积**至多**或**至少**则影响边界条件的判断，以求*方案数*为例，呈现对比如下：

```python
def dfs(i: int, c: int) -> int:
    if i < 0:
        return 1 if c == 0 else 0
    if c < weights[i]:
        return dfs(i-1, c)
    return dfs(i-1, c) + dfs(i-1, c-weights[i])
```
{: file="恰好" }

```python
def dfs(i: int, c: int) -> int:
    if i < 0:
        return 1
    if c < weights[i]:
        return dfs(i-1, c)
    return dfs(i-1, c) + dfs(i-1, c-weights[i])
```
{: file="至多" }

```python
def dfs(i: int, c: int) -> int:
    if i < 0:
        return 1 if c <= 0 else 0
    return dfs(i-1, c) + dfs(i-1, c-weights[i])
```
{: file="至少" }

### 空间复杂度优化
空间复杂度的优化主要沿着以下思路：
- 递归 转换为 递推（二维数组）
- 二维数组 转换为 两个数组
- 两个数组 转换为 一个数组

以**01 背包**中容量恰好等于`capacity`，求*方案数*为例。

```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> int:

    @cache
    def dfs(i: int, c: int) -> int:
        if i < 0:
            return 0
        if c < weights[i]:
            return dfs(i-1, c)
        return dfs(i-1, c) + dfs(i-1, c-weights[i])

    return dfs(len(weights)-1, capacity)
```
{: file="递归" }

```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> int:
    dp = [[0] * (capacity+1) for _ in range(len(weights)+1)]
    for i, w in enumerate(weights):
        for c in range(capacity+1):
            if c < w:
                dp[i+1][c] = dp[i][c]
            else:
                dp[i+1][c] = dp[i][c] + dp[i][c-w]
    return dp[len(weights)][capacity]
```
{: file="递推" }

```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> int:
    dp = [[0] * (capacity+1) for _ in range(2)]
    for i, w in enumerate(weights):
        for c in range(capacity+1):
            if c < w:
                dp[(i+1)%2][c] = dp[i%2][c]
            else:
                dp[(i+1)%2][c] = dp[i%2][c] + dp[i%2][c-w]
    return dp[n%2][capacity]
```
{: file="两个数组"}

```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> int:
    dp = [0] * (capacity+1)
    dp[0] = 1
    for w in weights:
        for c in range(capacity, w-1, -1):
            dp[c] = dp[c] + dp[c-w]
    return dp[capacity]
```
{: file="一个数组"}

> 仅使用“一个数组”实现时，需要特别注意循环的顺序——因为数据是一边写一边计算的。
>
> 当 $\text{dp}(i, c)$ 依赖于 $\text{dp}({\color{\red} i-1, c})$ 与 $\text{dp}({\color{\red} i-1, c-\Delta})$ 时，应当**逆序**；
>
> 当 $\text{dp}(i, c)$ 依赖于 $\text{dp}({\color{\red} i-1, c})$ 与 $\text{dp}({\color{\red} i, c-\Delta})$ 时，应当**正序**。
{: .prompt-warning}

当目标为*是否存在可行解*时，还可以进一步用 bitset 的位操作进行优化。我们先给出**01 背包**中容量恰好等于 `capacity`的*一个数组*的代码：

```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> bool:
    dp = [True] + [False] * capacity
    for w in weights:
        for c in range(capacity, w-1, -1):
            dp[c] = dp[c] or dp[c-w]
    return dp[capacity]
```
{: file="一个数组"}

转换为 bitset 时，难点在于理解递归公式为何可以使用位操作`dp |= dp >> w`实现。此时 `dp >> i & 1` 表示的是 `c=i` 的可行情况，它应当为 `dp[i]`（第`i`位置的布尔值） 与 `dp[i-w]`（第`i-w`位置的布尔值）的逻辑或；同时位操作相当于并行计算了所有 $[w, c]$ 的情况。

```python
def backpack(capacity: int, weights: list[int], values: list[int]) -> bool:
    dp = 1
    for w in weights:
        dp |= dp >> w
    return dp >> capacity & 1 == 1
```

> 该技巧不仅能优化空间复杂度，也能优化时间复杂度。
{: .prompt-info}

## 进阶
### 多重背包
物品可以重复选，有个数限制。

**题目清单**有：
- [2585. 获得分数的方法数](https://leetcode.cn/problems/number-of-ways-to-earn-points/description/)
- [3333. 找到初始输入字符串 II](https://leetcode.cn/problems/find-the-original-typed-string-ii/description/)
- [2902. 和带限制的子多重集合的数目](https://leetcode.cn/problems/count-of-sub-multisets-with-bounded-sum/description/)
- [3489. 零数组变换 IV](https://leetcode.cn/problems/zero-array-transformation-iv/description/)

### 分组背包
同一组内的物品至多/恰好选一个。

**题目清单**有：
- [1155. 掷骰子等于目标和的方法数](https://leetcode.cn/problems/number-of-dice-rolls-with-target-sum/description/)
- [1981. 最小化目标值与所选元素的差](https://leetcode.cn/problems/minimize-the-difference-between-target-and-chosen-elements/description/)
- [2218. 从栈中取出 K 个硬币的最大面值和](https://leetcode.cn/problems/maximum-value-of-k-coins-from-piles/description/)

### 树形背包
也叫树上背包、依赖背包等。
- [3562. 折扣价交易股票的最大利润](https://leetcode.cn/problems/maximum-profit-from-trading-stocks-with-discounts/description/)

## 参考
[0-1背包 完全背包](https://www.bilibili.com/video/BV16Y411v7Y6/)
