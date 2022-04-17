---
title: 理解动态规划
date: 2022-03-30 20:20:48
id: DP
categories:
- algo
tags:
- learn
---



动态规划，通过把原问题分解为相对简单的子问题的方式求解复杂问题的方法。

动态规划简介，核心思想，案例，解题思路。



<!-- more -->



#### 1 什么是动态规划

动态规划（Dynamic programming，DP），通过把原问题分解为相对简单的子问题的方式求解复杂问题的方法（自底向上）。动态规划常常适用于有重叠子问题和最优子结构性质的问题。

动态规划把子问题的答案保存起来，以减少重复计算。再根据子问题答案反推，得出原问题解的一种方法。

#### 2 核心思想

动态规划最核心的思想，就在于拆分子问题，记住过往，减少重复计算。

#### 3 例子

```
题目：
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
```

```go
// 方法一：暴力递归
// time limit
// 时间复杂度：O(2^n) 每次递归复杂度*2，一共有n次
func climbStairs(n int) int {
	if n <= 2 {
		return n
	}
	return climbStairs(n-1) + climbStairs(n-2)
}
```

```go
// 方法二：带备忘录的递归（自顶向下）
// 声明备忘录，记录计算过的答案 此时为nil
var memo map[int]int
func climbStairs(n int) int {
    // 申请一个空间
	if memo == nil {
		memo = make(map[int]int)
	}
    // 边界
	if n <= 2 {
		return n
	}
    // 备忘录中存在
	if tmp := memo[n]; tmp != 0 {
		return tmp
	}
    // 不存在
	memo[n] = climbStairs(n-1) + climbStairs(n-2)
	return memo[n]
}
```

```go
// 方法三：动态规划（自底向上）
// 最优子结构：f(n-1)，f(n-2)
// 状态转移方程：f(n) = f(n-1) + f(n-2)
// 边界：f(1) = 1，f(2) = 2
// 重叠子问题：f(10) = f(9) + f(8)，f(9) = f(8) + f(7)
func climbStairs(n int) int {
	if n <= 2 {
		return n
	}
	before1 := 1
	before2 := 2
	res := 0
	for i := 3; i <= n; i++ {
		res = before1 + before2
		before1 = before2
		before2 = res
	}
	return res
```



#### 4 解题思路

- 穷举分析
- 确定边界
- 找规律（确定最优子结构）
- 写出状态转移方程
