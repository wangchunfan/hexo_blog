---
title: 《剑指offer》面试题6：重建二叉树
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---


# 题目描述

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。


# 解法1：递归

思路：了解前序遍历和后序遍历的特征，前序遍历序列第一个元素为根节点后边为全部左子树节点+全部右子树节点；中序遍历序列根节点左面均为左子树节点，右边均为右子树节点
1. 通过前序遍历序列找到根节点 `val`
2. 通过 `val` 和中序遍历序列找到左子树序列长度 `len` ，得到了左子树的中序序列 和 右子树的中序序列
3. 通过 `len` 获取前序遍历序列中的左子树前序序列 和 右子树前序序列
4. 重复 1 2 3 步骤，每次返回一个根节点，终止条件 `len == 0`，或者是由子树长度为0

![操作](https://note.youdao.com/yws/public/resource/03dfd851f24b216e58d1d651eff575ae/xmlnote/50440AC550554F8D9F3DD2338662F80C/4667)

## 每次获取新的前序遍历和中序遍历的全部内容去递归

```js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function reConstructBinaryTree(pre, vin)
{
    // write code here
    if (!pre|| !vin || pre.length == 0 || vin.length == 0)
        return null;
    return binaryTreeCore(pre, 0, pre.length - 1, vin, 0, vin.length - 1);
}

function binaryTreeCore(pre, preStart, preEnd, vin, vinStart, vinEnd) {
    var rootVal = pre[preStart];
    var rootIndex = vin.indexOf(rootVal);
    var treeNode = new TreeNode(rootVal);
    if (vinStart < rootIndex) treeNode.left = binaryTreeCore(pre, preStart + 1, rootIndex - vinStart + preStart, vin, vinStart, rootIndex - 1);
    if (rootIndex < vinEnd) treeNode.right = binaryTreeCore(pre, rootIndex - vinStart + preStart + 1, preEnd, vin, rootIndex + 1, vinEnd);
    return treeNode;
}
```

## 每次用 根节点 和 中序序列 去递归

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode reConstructBinaryTree(int[] pre, int[] in) {
        if (pre == null || in == null || pre.length == 0 || in.length == 0)
            return null;
        return binaryTree(pre, in, 0, 0, in.length - 1);
    }

    public TreeNode binaryTree(int[] pre, int[] in, int rootIndex, int inStart, int inEnd) {
        int rootVal = pre[rootIndex];
        TreeNode treeNode = new TreeNode(rootVal);
        for (int i = inStart; i <= inEnd; i++) {
            if (in[i] == rootVal) {
                                                                     //注意不要使用 ++rootIndex，因为下一步会用到rootIndex
                if (i > inStart) treeNode.left = binaryTree(pre, in, rootIndex + 1, inStart, i - 1);
                if (i < inEnd) treeNode.right = binaryTree(pre, in, i - inStart + rootIndex + 1, i + 1, inEnd);
            }
        }
        return treeNode;
    }
}

```