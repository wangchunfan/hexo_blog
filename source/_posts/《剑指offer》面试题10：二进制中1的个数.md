---
title: 《剑指offer》面试题10：二进制中1的个数
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---


# 算法描述

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

# 解法1：可能引起死循环的解法

输入的数n与1做与运算，1的左边位均为0，做与运算结果为0；结果为0或者1就看末位是0或者1

|输入n| 1| 0| 1|0| 1|
|-|-|-|-|-|-|
|    1| 0| 0| 0|0| 1|   
|结果 | 0| 0| 0|0| 1|

主要问题出在 `n >> 1`上面，负数的左移是在左边补`1`，导致死循环

```js
function NumberOf1(n)
{
    // write code here
    var count = 0;
    while (n) {
       if (n & 1)
         count ++;
       n = n >> 1;
    }
    return count;
}
```


# 解法2：常规解法

将`1`左移一位，与n做与运算，32位的二进制数，左移32次后变成0

|输入n| 1| 0| 1|0| 1|
|-|-|-|-|-|-|
|    1| 0| 0| 1|0| 0|   
|结果 | 0| 0| 1|0| 0|

```js
function NumberOf1(n)
{
    // write code here
    var count = 0;
    var i = 1;
    while (i) {
       if (n & i)
         count ++;
       i = i << 1;
    }
    return count;
}

```

# 解法3：最优解法

发现规律，对于二进制数①，将其-1后得到②，再用①与②做与运算，得到的结果刚好少了一位1

![规律](https://note.youdao.com/yws/public/resource/03dfd851f24b216e58d1d651eff575ae/xmlnote/1B30447DB0AC446BAE603DCEDB8816CA/4978)

```
//.js
function NumberOf1(n)
{
    // write code here
    //不等于0
    var count = 0;
    while(n) {
        count ++;
        n = n & (n - 1);
    }
    return count;
}
```

```java
//.java
public class Solution {
    public int NumberOf1(int n) {
        int count = 0;
        while (n != 0) {
            count++;
            n = n & (n - 1);
        }
        return count;
    }
}

```