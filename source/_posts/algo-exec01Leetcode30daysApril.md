---
title: Leetcode30天算法挑战
date: 2021-03-28 22:30:00
id: leetcode1
categories:
- algo
tags:
- exec
---

leetcod的一个算法练习计划，一天一道算法题，一共30道题。

跟着[Feis Studio](https://feis.studio/#/)的Feis Lee老师学的。视频链接：[【C 語言的 LeetCode 30 天挑戰】](https://www.bilibili.com/video/BV1764y1M7a6?spm_id_from=..search-card.all.click)

实现语言：C

<!-- more -->

## April



### 53. Maximum Subarray

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

A **subarray** is a **contiguous** part of an array.

 

**Example 1:**

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Solution:**

```c
int cmp(int a, int b){
    return (a > b) ? a : b;
}

int maxSubArray(int* nums, int numsSize){
    int pre = 0;
    int max = nums[0];
    
    for(int i = 0; i < numsSize; i++) {
        pre = cmp(pre + nums[i], nums[i]);
        max = cmp(pre, max);
    }

    return max;
}
```





### 136. Single Number

Given a **non-empty** array of integers `nums`, every element appears *twice* except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

 

**Example 1:**

```
Input: nums = [2,2,1]
Output: 1
```

**Solution:**

```c
// 经典异或题目

int singleNumber(int* nums, int numsSize) {   
    
    for (int i = 1; i < numsSize; i++) {
        
        nums[0] = nums[0] ^ nums[i];
        
    }    
    
    return nums[0];
}
```





### 202. Happy Number

Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

-   Starting with any positive integer, replace the number by the sum of the squares of its digits.
-   Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
-   Those numbers for which this process **ends in 1** are happy.

Return `true` *if* `n` *is a happy number, and* `false` *if not*.

 

**Example 1:**

```
Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

**Solution:**

```c
// 龟兔赛跑 slow fast

int next(int n) {
    int n1 = 0;
    while(n != 0) {
        n1 += (n % 10) * (n % 10);
        n /= 10;
    }
    return n1;
}


bool isHappy(int n){
    int slow = n;
    int fast = next(n);
    while (slow != fast && fast != 1) {
        slow = next(slow);
        fast = next(next(fast));
    }
    if (fast == 1) return true;
    return false;
}
```





### 283. Move Zeroes

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

 

**Example 1:**

```
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Solution:**

```c
void swap(int *a, int *b) {
    int t = *a;
    *a = *b, *b = t;
}

void moveZeroes(int *nums, int numsSize) {
    int left = 0, right = 0;
    while (right < numsSize) {
        if (nums[right]) {
            swap(nums + left, nums + right);
            left++;
        }
        right++;
    }
}
```





### 122. Best Time to Buy and Sell Stock II

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return *the **maximum** profit you can achieve*.

 

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```

**Solution 1:**

```c
// The Limit Exceeded

int maxProfit(int* prices, int pricesSize){
    
    if (pricesSize <= 1) return 0;
    
    int profit;
    int max = 0;
    
    // 最后一天不卖
    profit = maxProfit(prices, pricesSize - 1);
    if (profit > max) max = profit;
    
    // 最后一天卖
    for (int i = 0; i < pricesSize - 1; i++) {
        profit = prices[pricesSize - 1] - prices[i] + maxProfit(prices, i);
        if (profit > max) max = profit;
    }
     
    return max;
}
```

**Solution 2: Peak Valley Approach**

![](https://zhenruyi.github.io/images/algo02Leetcode30daysApril122_1.png)

```c
// 所有波峰加波谷之和

int maxProfit(int* prices, int pricesSize){
    int i = 1;
    int valley = prices[0];
    int peak = prices[0];
    int profit = 0;
    
    while(i < pricesSize) {
        while(i < pricesSize && prices[i] <= prices[i-1])
            i++;
        valley = prices[i-1];
        
        while(i < pricesSize && prices[i] >= prices[i-1])
            i++;
        peak = prices[i-1];
        profit += peak - valley;
    }
    return profit;
}
```

改进：

![](https://zhenruyi.github.io/images/algo02Leetcode30daysApril122_2.png)

```java
JAVA:

class Solution {
    public int maxProfit(int[] prices) {
        int maxprofit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1])
                maxprofit += prices[i] - prices[i - 1];
        }
        return maxprofit;
    }
}
```

**Solution 2: 乐扣**

```c
// 动态规划
// 0:手中没有股票, 1:手中有股票
int maxProfit(int* prices, int pricesSize){
    int profit[pricesSize][2];
    // 手中没有股票
    profit[0][0] = 0;
    // 手中有股票
    profit[0][1] = -prices[0];
    
    for(int i=1; i<pricesSize; i++) {
        profit[i][0] = profit[i-1][0] > (profit[i-1][1]+prices[i]) ? profit[i-1][0] : (profit[i-1][1]+prices[i]);
        profit[i][1] = profit[i-1][1] > (profit[i-1][0]-prices[i]) ? profit[i-1][1] : (profit[i-1][0]-prices[i]);
    }
    
    return profit[pricesSize - 1][0];
}
```

```c
// 贪心算法
// 在每个区间都是获得利润
int maxProfit(int* prices, int pricesSize){
    int profit = 0;
    
    for(int i = 1; i < pricesSize; i++) {
        profit += (prices[i] - prices[i-1] > 0) ? prices[i] - prices[i-1] : 0;
    }
    return profit;
}
```







### 49. Group Anagrams

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

**Example 1:**

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**Solution 1:**

用质数表示26个字母，把字符串的各个字母相乘，这样可保证字母异位词的乘积必定是相等的。其余步骤就是用map存储，和别人的一致了。





### 876. Middle of the Linked List

Given the `head` of a singly linked list, return *the middle node of the linked list*.

If there are two middle nodes, return **the second middle** node.



**Solution 1:**

```c
struct ListNode* middleNode(struct ListNode* head){
    int nodeSize = 0;
    struct ListNode* p = head;
    while(p != NULL) {
        nodeSize++;
        p = p->next;
    }
    
    nodeSize /= 2;
    for(int i=0; i<nodeSize; i++) {
        head = head->next;
    }
    return head;
}
```

**Solution 2: 快慢指针，快的比慢的快两倍**

```c
struct ListNode* middleNode(struct ListNode* head){
    struct ListNode *fast, *slow;
    fast = head;
    slow = head;
    while(fast->next != NULL && fast != NULL) {
        if(fast->next->next == NULL)
            return slow->next;
        fast = fast->next->next;
        slow = slow->next;
    }
    return slow;
}
```





### 844. Backspace String Compare

Given two strings `s` and `t`, return `true` *if they are equal when both are typed into empty text editors*. `'#'` means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

 

**Example 1:**

```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```

**Solution 1: 重构字符串**

```c
bool backspaceCompare(char * s, char * t){
    char sNew[201];
    char tNew[201];
    
    int i = 0;
    int j = 0;
    while(s[i] != '\0') {
        if(s[i] == '#') {
            if(j > 0)
                j--;
            i++;
            continue;
        }
        sNew[j] = s[i];
        j++;
        i++;
    }
    sNew[j] = '\0';
    
    i = 0;
    j = 0;
    while(t[i] != '\0') {
        if(t[i] == '#') {
            if(j > 0)
                j--;
            i++;
            continue;
        }
        tNew[j] = t[i];
        j++;
        i++;
    }
    tNew[j] = '\0';
    
    i = 0;
    while(sNew[i] != '\0' || tNew[i] != '\0') {
        if(sNew[i] != tNew[i])
            return false;
    	i++;
    }
    return true;
}
```

**Solution 2: 双指针**

```c
bool backspaceCompare(char * s, char * t){
    int ps = strlen(s) - 1;
    int pt = strlen(t) - 1;
    int sSkip = 0, tSkip = 0;
    
    while(ps >= 0 || pt >= 0) {
        while(ps >= 0) {
            if(s[ps] == '#') {
                ps--;
                sSkip++;
            } else if(sSkip > 0) {
                ps--;
                sSkip--;
            } else {
                break;
            }
        }
        
        while(pt >= 0) {
            if(t[pt] == '#') {
                pt--;
                tSkip++;
            } else if (tSkip > 0) {
                pt--;
                tSkip--;
            } else {
                break;
            }
        }
        
        if (pt >= 0 && ps >= 0) {
            if (s[ps] != t[pt]) {
                return false;
            }
        } else {
            if (ps >= 0 || pt >= 0) {
                return false;
            }
        }
        ps--, pt--;
    }
    return true;
}
```





### 155. Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

-   `MinStack()` initializes the stack object.
-   `void push(int val)` pushes the element `val` onto the stack.
-   `void pop()` removes the element on the top of the stack.
-   `int top()` gets the top element of the stack.
-   `int getMin()` retrieves the minimum element in the stack.

 

**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

**Solution 1:**

```c
typedef struct {
    int* data;
    int* mins;
    int size;
} MinStack;


MinStack* minStackCreate() {
    MinStack* s = malloc(sizeof(MinStack));
    s->data = NULL;
    s->mins = NULL;
    s->size = 0;
    return s;
}

void minStackPush(MinStack* obj, int val) {
    obj->size++;
    obj->data = realloc(obj->data, sizeof(int)*(obj->size));
    obj->mins = realloc(obj->mins, sizeof(int)*(obj->size));
    obj->data[obj->size-1] = val;
    if(obj->size == 1) {
        obj->mins[obj->size-1] = val;
    } else {
        if(val < obj->mins[obj->size-2]) {
            obj->mins[obj->size-1] = val;
        } else {
            obj->mins[obj->size-1] = obj->mins[obj->size-2];
        }
    }
}

void minStackPop(MinStack* obj) {
    obj->size--;
}

int minStackTop(MinStack* obj) {
    return obj->data[obj->size-1];
}

int minStackGetMin(MinStack* obj) {
    return obj->mins[obj->size-1];
}

void minStackFree(MinStack* obj) {
    free(obj->data);
    free(obj->mins);
    free(obj);
}
```

**Solution 2: 辅助栈：力扣**





### 543. Diameter of Binary Tree

Given the `root` of a binary tree, return *the length of the **diameter** of the tree*.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.



**Solution 1:**

```c
// 假定一个结点root，先求出左枝最大深度，再求右枝最大深度，相加就是最大半径
// 最大半径不一定经过root，求出所有结点的最大半径，再比较就可以。

int maxDepth(struct TreeNode* root) {
    if(root == NULL) return 0;
    
    int left = maxDepth(root->left) + 1;
    int right = maxDepth(root->right) + 1;
    
    if(left > right) return left;
    return right;
}


int diameterOfBinaryTree(struct TreeNode* root){
    
    if(root == NULL) return 0;
    
    int leftDep = maxDepth(root->left);
    int rightDep = maxDepth(root->right);
    int middleDia = leftDep + rightDep;
    int maxDia = middleDia;
    
    int leftDia = diameterOfBinaryTree(root->left);
    int rightDia = diameterOfBinaryTree(root->right);
    
    if(leftDia > maxDia) maxDia = leftDia;
    if(rightDia > maxDia) maxDia = rightDia;
    
    return maxDia;
}
```





### 1046. Last Stone Weight

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:

-   If `x == y`, both stones are destroyed, and
-   If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return *the smallest possible weight of the left stone*. If there are no stones left, return `0`.

 

**Example 1:**

```
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation: 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.
```

**Solution 1:**

```c
// 返回最大重量
int findBig(int* stonesN) {
    for(int i = 1000; i > 0; i--) {
        if(stonesN[i] > 0) {
            stonesN[i]--;
            return i;
        }
    }
    return 0;
}

int lastStoneWeight(int* stones, int stonesSize){
    // 该重量的石头有几个？
    int stonesN[1001] = {0};
    for(int i = 0; i < stonesSize; i++) {
        stonesN[stones[i]]++;
    }
    // 最大重量y，第二大重量x
    int y = findBig(stonesN);
    int x = findBig(stonesN);
    
    while(x != 0) {
        // 摧毁之后再放回去
        stonesN[y-x]++;
        y = findBig(stonesN);
        x = findBig(stonesN);
    }
    return y;
}
```





### 525. Contiguous Array

Given a binary array `nums`, return *the maximum length of a contiguous subarray with an equal number of* `0` *and* `1`.

 

**Example 1:**

```
Input: nums = [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with an equal number of 0 and 1.
```

**Example 2:**

```
Input: nums = [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Solution 1: 前缀和**

```c
// Time Limit Exceeded
int findMaxLength(int* nums, int numsSize){
    
    for(int i = 0; i < numsSize; i++)
        if(nums[i] == 0) nums[i] = -1;

    int perSum[numsSize + 1];
    perSum[0] = 0;
    int counter = 0;
    for(int i = 0; i < numsSize; i++) {
        counter += nums[i];
        perSum[i + 1] = counter;
    }
    
    int maxLen = 0;
    for(int i = 0; i < numsSize; i++) {
        int len = 0;
        for(int j = numsSize; j >= i; j--) {
            if(perSum[i] == perSum[j]) {
                len = j - i;
                break;
            }
        }
        if(len > maxLen) maxLen = len;
    }
    return maxLen;
}
```

**Solution 2: 前缀和+哈希表**







### 238. Product of Array Except Self

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

 

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Example 2:**

```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

**Constraints:**

-   `2 <= nums.length <= 105`
-   `-30 <= nums[i] <= 30`
-   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Solution 1:**

```c
int* productExceptSelf(int* nums, int numsSize, int* returnSize){
    int prefix[numsSize];
    int suffix[numsSize];
    int* ans = malloc(sizeof(int) * numsSize);
    *returnSize = numsSize;
    
    prefix[0] = nums[0];
    for(int i = 1; i < numsSize-1; i++) {
        prefix[i] = prefix[i-1] * nums[i];
    }
    
    suffix[numsSize-1] = nums[numsSize-1];
    for(int i = numsSize-2; i > 0; i--) {
        suffix[i] = suffix[i+1] * nums[i];
    }
    
    ans[0] = suffix[1];
    ans[numsSize-1] = prefix[numsSize-2];
    for(int i = 1; i < numsSize - 1; i++) {
        ans[i] = prefix[i-1] * suffix[i+1];
    }
    return ans;
}
```

**Solution 2: **

```c
int* productExceptSelf(int* nums, int numsSize, int* returnSize){
    *returnSize = numsSize;
    
    int* ans = malloc(sizeof(int) * numsSize);
    int left=1, right=1;
    
    for(int i=0; i < numsSize; i++)
        ans[i] = 1;
    
    for(int i=0; i<numsSize; i++) {
        ans[i] *= left;
        left *= nums[i];
        
        ans[numsSize-1-i] *= right;
        right *= nums[numsSize-1-i];
    }
    return ans;
}
```







### 20. Valid Parentheses

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.

 

**Example 1:**

```
Input: s = "()"
Output: true
```

**Example 2:**

```
Input: s = "()[]{}"
Output: true
```

**Example 3:**

```
Input: s = "(]"
Output: false
```

**Example 4:**

```
Input: s = "([)]"
Output: false
```

**Example 5:**

```
Input: s = "{[]}"
Output: true
```

**Solution 1: 栈**

```c
int trans(char ch) {
    if(ch == '}') return '{';
    if(ch == ']') return '[';
    if(ch == ')') return '(';
    return 0;
}

bool isValid(char * s){
    int len = strlen(s);
    int top = 0;
    int stack[len];
    int ch;
    
    for(int i = 0; i < len; i++) {
        ch = trans(s[i]);
        if(ch) {
            top--;
            if(top < 0 || stack[top] != ch) return false;  
        } else {
            stack[top++] = s[i];
        }
    }
    return top == 0;
}
```

