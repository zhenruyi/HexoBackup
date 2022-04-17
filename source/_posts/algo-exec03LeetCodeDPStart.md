---
title: Leetcode 动态规划入门
date: 2022-03-30 22:49:56
id: leetcode3
categories:
- algo
tags:
- exec
---



Leetcode上的动态规划学习计划。

最近备战蓝桥杯，所以用C实现的。



<!-- more -->



#### 509 斐波那契数

斐波那契数 （通常用 F(n) 表示）形成的序列称为斐波那契数列。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
给定 n ，请计算 F(n) 。

```c
int fib(int n) {
    if(n <= 1) return n;
    int pre1 = 0;
    int pre2 = 1;
    int res = 0;
    for(int i = 2; i <= n; i++) {
        res = pre1 + pre2;
        pre1 = pre2;
        pre2 = res;
    }
    return res;
}
```



#### 1137 第N个泰波那锲数

泰波那契序列 Tn 定义如下： 
T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2
给你整数 n，请返回第 n 个泰波那契数 Tn 的值。

```c
int tribonacci(int n){
    if(n == 0) return 0;
    if(n <= 2) return 1;
    int t1 = 0;
    int t2 = 1;
    int t3 = 1;
    int res = 0;
    for(int i = 3; i <= n; i++) {
        res = t1 + t2 + t3;
        t1 = t2;
        t2 = t3;
        t3 = res;
    }
    return res;
}
```



#### 746 使用最小花费爬楼梯

给你一个整数数组 cost ，其中 cost[i] 是从楼梯第 i 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。
你可以选择从下标为 0 或下标为 1 的台阶开始爬楼梯。
请你计算并返回达到楼梯顶部的最低花费。

```c
int minCostClimbingStairs(int* cost, int costSize){
    if(costSize == 2) return cost[0] < cost[1] ? cost[0] : cost[1];
    int pre1 = cost[0];
    int pre2 = cost[1];
    int min = 0;
    for(int i = 2; i < costSize; i++) {
        if(pre1 < pre2) min = pre1;
        else min = pre2;
        pre1 = pre2;
        pre2 = min+cost[i];
    }
    if(pre1 < pre2) return pre1;
    return pre2;
}
```



#### 198 打家劫舍

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。
给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。

```c
int rob(int* nums, int numsSize){

    if(numsSize == 1) return nums[0];
    if(numsSize == 2) return nums[0] > nums[1] ? nums[0] : nums[1];

    int pre1 = nums[1];
    int pre2 = nums[0];
    int pre3 = 0;
    int max = 0;
    
    for(int i=2; i < numsSize; i++) {
        if(pre3 > pre2) max = pre3;
        else max = pre2;
        pre3 = pre2;
        pre2 = pre1; 
        pre1 = max + nums[i];
    }
    return pre1 > pre2 ? pre1 : pre2;

}
```



#### 213 打家劫舍2

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都围成一圈，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。
给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，今晚能够偷窃到的最高金额。

```c
int rob(int* nums, int numsSize){
    // 分成两个数组，一个除去第一个元素，一个除去最后一个元素。

    if(numsSize == 1) return nums[0];
    if(numsSize == 2) return nums[0] > nums[1] ? nums[0] : nums[1];

    int first = nums[0];
    int second = nums[0] > nums[1] ? nums[0] : nums[1];
    for(int i=2; i < numsSize-1; i++) {
        int tmp = first;
        first = second;
        second = (tmp + nums[i]) > second ? (tmp + nums[i]) : second;
    }
    int max = second;
    first = nums[1];
    second = nums[1] > nums[2] ? nums[1] : nums[2];
    for(int i=3; i < numsSize; i++) {
        int tmp = first;
        first = second;
        second = (tmp + nums[i]) > second ? (tmp + nums[i]) : second;
    }
    return second > max ? second : max;

}
```



#### 740 删除并获得点数

给你一个整数数组 nums ，你可以对它进行一些操作。

每次操作中，选择任意一个 nums[i] ，删除它并获得 nums[i] 的点数。之后，你必须删除 所有 等于 nums[i] - 1 和 nums[i] + 1 的元素。

开始你拥有 0 个点数。返回你能通过这些操作获得的最大点数。

```go
// 我写的代码
func deleteAndEarn(nums []int) int {
	length := len(nums)
	if length == 1 {
		return nums[0]
	}
	if length == 2 {
		if (nums[0] - nums[1]) * (nums[0] - nums[1]) == 1 {
			if nums[0] > nums[1] {
				return nums[0]
			}
			return nums[1]
		}
		return nums[0] + nums[1]
	}

	total := map[int]int{}
	max := nums[0]
	for i:=0; i < length; i++ {
		num := nums[i]
		total[num] += num
		if num > max {
			max = num
		}
	}
	pre1 := 0
	pre2 := total[0]
	pre3 := total[1]
	res := total[2]
	m := 0
	for i:=2; i <=max; i++ {
		res = total[i]
		if pre1 > pre2 {
			m = pre1
		} else {
			m = pre2
		}
		res += m
		pre1 = pre2
		pre2 = pre3
		pre3 = res
	}
	if pre3 > pre2 {
		return pre3
	}
	return pre2
}
```

```go
// 优化之后
func deleteAndEarn(nums []int) int {
	maxValue := nums[0]
	for _, value := range nums {
		if value > maxValue {
			maxValue = value
		}
	}
	total := make([]int, maxValue+1)
	for _, value := range nums {
		total[value] += value
	}
	return rob(total)
}

func rob(nums []int) int {
	first := nums[0]
	second := max(nums[0], nums[1])
	for i:=2; i<len(nums); i++ {
		first, second = second, max(first+nums[i], second)
	}
	return second
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```



#### 55 跳跃游戏

给定一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标。

```go
func canJump(nums []int) bool {
	farthestJump := nums[0]
	for i := 1; i < len(nums); i++ {
		farthestJump--
		if farthestJump < 0 {
			return false
		}
		farthestJump = max(farthestJump, nums[i])
	}
	return true
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

