---
title: 《剑指offer》面试题5：从尾到头打印链表
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---

# 题目描述

输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。


# 解法1：顺序遍历

最简单的方法就是对链表进行顺序遍历，需要借助`JavaScript`数组的几个内置的方法

## `Array.reverse()`

顺序遍历，将值放到数组中，对数组进行翻转

```js
function printListFromTailToHead(head)
{
    // write code here
    var res = [];
    while(head != null){
        res.push(head.val);
        head = head.next;
    }
    return res.reverse();
}
```

## `Array.unshift`

`unshift`是在数组头部插入元素，与`push`正好相反
```js
function printListFromTailToHead(head)
{
    // write code here
    var res = [];
    while(head != null){
        res.unshift(head.val);
        head = head.next;
    }
    return res;
}
```

# 解法2：反转节点的指针




# 解法3：递归

- 每次都将对上一次返回的数组进行`push`操作,插入当前元素
- 终止点返回的数组为[]，从后向前插入元素

```js
//.js
function printListFromTailToHead(head)
{
    // write code here
    var res = [];
    if (head != null){
        res = printListFromTailToHead(head.next);
        res.push(head.val);
    }
    return res;
}
```

注意Java中使用ArrayList.add()
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> arrayList = new ArrayList<Integer>();
        if (listNode != null){
            arrayList = printListFromTailToHead(listNode.next);
            arrayList.add(listNode.val);
        }
        return arrayList;
    }
}
```

