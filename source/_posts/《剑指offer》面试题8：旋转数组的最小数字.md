---
title: 《剑指offer》面试题8：旋转数组的最小数字
toc: true
comments: true
tags: "《剑指offer》"
categories: "刷刷题/《剑指offer》"
---


# 题目描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

# 解法1：二分查找

规律：
- left>=right
- 如果`Array[mid]>=Array[left]`,说明是left与midz之间是顺序序列，最小值不在left与mid之间那么left=mid;否则right=mid
- 只有left的移动（left = mid）才能导致`Array[left] < Array[right]`的出现
- 特列：如果`left==mid==right`,只能顺序查找

![举例](https://note.youdao.com/yws/public/resource/03dfd851f24b216e58d1d651eff575ae/xmlnote/8C618984A27D41E880A46BCCF450BD60/4811)

```
//.js 注意 JavaScript语言中 3/2 = 1.5 需要使用parseInt(1.5) = 1
function minNumberInRotateArray(rotateArray)
{
    // write code here
    if(rotateArray.length == 0)
        return 0;
    var left = 0;
    var right = rotateArray.length - 1;
    var mid = left;
    //特例情况
    if (left == right && left == mid && mid == right) {
        while (left < rotateArray.length() - 1 && rotateArray[left] >= rotateArray[right] ) {
            left ++
        }
        return rotateArray[left];
    }
    //二分查找
    while (rotateArray[left] >= rotateArray[right]){
        if (left + 1 == right) {
            mid = right;
            break;
        }
        mid = parseInt((left + right) / 2);
        if (rotateArray[mid] >= rotateArray[left]) 
            left = mid;
        else 
            right = mid;
    }
    return rotateArray[mid];
    
}

```
解题时要注意比较的是`Array[left] Array[right]`不要比较成下标`left right`

```java
//.java
public class Solution {
    public int minNumberInRotateArray(int[] array) {
        if (array.length == 0)
            return 0;
        int left = 0;
        int right = array.length - 1;
        int mid = left;
        if (array[left] == array[right] && array[left] == array[mid] && array[right] == array[mid]) {
            for (int i = left; i < right; i++) {
                if (array[i] < array[right])
                    return array[i];
            }
            return array[mid];
        }
        while (array[left] >= array[right]) {
            if (left + 1 == right) {
                mid = right;
                break;
            }
            mid = (left + right) / 2;
            if (array[mid] >= array[left])
                left = mid;
            else
                right = mid;
        }
        return array[mid];

    }
}
```