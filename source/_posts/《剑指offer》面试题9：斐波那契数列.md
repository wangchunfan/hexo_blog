---
title: 《剑指offer》面试题9：斐波那契数列
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---


# 问题描述

大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。
n<=39

# 解放1：递归

```java
/.java
public class Solution {
    public int Fibonacci(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        return Fibonacci(n - 1) + Fibonacci(n - 2);
    }
}
```


# 解法2：动态规划

将前两次计算出来的值保存起来

```
/.js
function Fibonacci(n)
{
    // write code here
    if(n == 0)
        return 0;
    if(n == 1)
        return 1;
    var temp1 = 0;
    var temp2 = 1;
    var result = 0;
    for (var i = 2;i <= n; i++) {
        result = temp1 + temp2;
        temp1 = temp2;
        temp2 = result;
    }
    return result;
}
```
时间复杂度:O(n)

# 解法3：矩阵的乘方

# 扩展

一只青蛙一次可以跳上1级或者2级或者...n级，此时该青蛙上一个n级的台阶总共有多少种跳法

用数学归纳法证明

# 相关题目

