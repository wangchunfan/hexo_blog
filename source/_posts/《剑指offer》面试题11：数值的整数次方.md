---
title: 《剑指offer》面试题11：数值的整数次方
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---


# 题目描述

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

注意：
>Math.pow(-2,2) = 4   (-2)^2 = -4

>Math.pow(-2,3) = -8

# 解法1：只考虑了指数为正数

```js
function Power(base, exponent)
{
    var result = base;
    // write code here
    for (var i = 2; i <= exponent; i ++) {
        result = result * base;
    }
    return result;
}
```


# 解法2：全面正确的方案

需要考虑`exponent` 的符号位和为0的情况:为0输出1,为负输出 `1 / result` ;

```js
function Power(base, exponent)
{
    var flag = false;
    if (exponent < 0) {
        flag = true;
        exponent = - exponent;
    }

    var result = 1;
    
    // write code here
    for (var i = 1; i <= exponent; i ++) {
        result = result * base;
    }
    if (flag)
        result = 1/result;
    return result;
}

```

# 解法3：递归

可以考虑a的8次方=a的4次方的平方

用 `>>` 来代替除以 `/` 2

用 `&` 代替求余数 `%` 运算

需要考虑`exponent` 的符号位和为0的情况:为0输出1,为负输出 `1 / result` ;


![递归公式](https://note.youdao.com/yws/public/resource/03dfd851f24b216e58d1d651eff575ae/xmlnote/9E9963DA8CF14B5DB0CC39E2D1130E02/5099)

```java
public class Solution {
    public double Power(double base, int exponent) {
        if (exponent == 1)
            return base;
        if (exponent == 0)
            return 1;
        double result = Power(base, (exponent < 0 ? -exponent : exponent) >> 1);//左移代替除以2
        result *= result;
        if ((exponent & 1) == 1) //奇数
            result *= base;
        return exponent < 0 ? 1 / result : result;
    }
}
```
