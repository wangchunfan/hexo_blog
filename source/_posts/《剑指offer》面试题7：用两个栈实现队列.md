---
title: 《剑指offer》面试题7：用两个栈实现队列
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---

# 题目描述

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

# 解法1

- 入栈：向栈1中插入
- 出栈：判断栈2是否为空
    - 空：栈1元素全部压入栈2
    - 栈2出栈

![操作过程](https://note.youdao.com/yws/public/resource/03dfd851f24b216e58d1d651eff575ae/xmlnote/376693303C8E4EDCA05CC87D8BB9EE33/4690)

```js
//.js
var stack1 = [];
var stack2 = [];
function push(node)
{
    // write code here
    stack1.push(node);
}
function pop()
{
    // write code here
    if(stack2.length == 0){
        while(stack1.length > 0){
            stack2.push(stack1.pop());
        }
    }
    if(stack2.length >= 0){
       return stack2.pop();
    }
}
```

```java
//.java
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();

    public void push(int node) {
        stack1.push(node);
    }

    public int pop() {
        if (stack2.size() == 0) {
            while (stack1.size() > 0) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }
}
```