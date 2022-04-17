---
title: 2022年2月刷的几类Leetcode题
date: 2022-02-01 23:00:00
id: leetcode2
categories:
- algo
tags:
- exec
---



2022年2月刷的几类Leetcode题：Binary Search，Two Pointers，Sliding Window。



<!-- more -->



Algorithm 1

1. Binary Search

   ```
   总结
   1. 用于查找 某个元素的位置 不产生新的集合
   2. 输入：已经排好序的集合 目标元素
   3. 输出：目标元素的位置
   4. 时间复杂度：O(log n)
   ```

   ```
   题目
   1. Binary Search
   Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.
   经典的二分查找
   
   2. First Bad Version
   Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.
   You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.
   提示：先把具体情况列出来，然后分析mid在不同情况下left和right的变化情况
   
   3. Search Insert Position
   Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
   You must write an algorithm with O(log n) runtime complexity.
   情况很多，所以可以返回right
   ```

   

2. Two Pointers

   ```
   总结
   1. 会产生一个新的集合，然后输出这个集合。
   2. 集合可以分段，例如分成正负数两段。
   3. 输入：一个集合
   4. 输出：符合要求的集合
   ```

   ```
   题目
   1. Squares of a Sorted Array
   Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.
   Input: nums = [-4,-1,0,3,10]
   Output: [0,1,9,16,100]
   分成正负两段，然后分别用不同的指针处理。
   知道集合长度的话，不一定要正序的，还可以倒序处理。
   
   2. Rotate Array
   Given an array, rotate the array to the right by k steps, where k is non-negative.
   Input: nums = [1,2,3,4,5,6,7], k = 3
   Output: [5,6,7,1,2,3,4]
   小心k>n，处理：k = k % n
   一种方法是建立一个临时数组，长度为k
   另一种方法是，分成1234和567两段，然后分别逆转
   
   3. Move Zeroes
   Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
   一种方法是先覆盖零，最后在结尾补充。用两个指针（一个指向遍历到的位置，一个是除去零该元素应该在的位置）。
   另一种方法是两个指针，一个指向零，另一个遍历，如果遇到非零，则和当前零交换位置。
   
   4. Two Sum II - Input Array Is Sorted
   给一个已经排好序的数组，然后找到两个数之和为目标数的位置。
   
   5. Middle of the Linked List
   快慢指针
   ```

   

3. Sliding Window

   ```
   总结
   1. 窗口：一组连续元素
   ```

   ```
   题目
   1. Longest Substring Without Repeating Characters
   Given a string s, find the length of the longest substring without repeating characters.
   用一个数组记录元素出现的次数，如果重复的话，则窗口移动。
   
   2. Permutation in String
   Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.
   In other words, return true if one of s1's permutations is the substring of s2.
   两个数组存字符串，最后不断移动窗口，找到数组1==数组2的地方。
   ```

   

