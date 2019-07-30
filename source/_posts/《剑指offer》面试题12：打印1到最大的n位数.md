---
title: 《剑指offer》面试题12：打印1到最大的n位数
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---

# 题目描述

输入n，按顺序打印出从1最大的n位十进制。比如输入3，则打印出1、2、3一直到最大的3位数即999.

# 解法1：未考虑大数

- 首先求出n+1位的最小值 maxValue = 1000..
- 从1开始依次输出小于maxValue的值
- maxValue的位数有限制，使用int?double?都不合适

```java
public class Solution {
    public void print1ton(int n) {
        if (n <= 0)
            return;
        int maxValue = 1;
        for (int i = 0; i < n; i++)
            maxValue *= 10;
        while (n < maxValue)
            System.out.println(n++);

    }
}

```

# 解法2：使用String表示大数

可以考虑使用字符串或者数组



# 解法3：使用递归