---
layout: post
title: 循环数组的查找
description: 
published: true
category: CS basic
---


## 1. 旋转数组中, 查询元素

基本思路:

* 分治: 二分查找, 划分为子问题

示例代码:

    /**
     * 从有序的「旋转数组」中, 查找指定的取值, 返回对应的下标。
     *
     * @param array 有序的旋转数组
     * @param destValue 目标值
     * @return 如果目标值存在, 则, 返回指定的下标
     */
    public static int findValue(int[] array, int destValue) {
        // 1. 边界判断
        if (null == array) {
            return -1;
        }

        // 2. 查找目标取值
        return binarySearch(array, 0, array.length - 1, destValue);
    }

    public static int binarySearch(int[] array, int start, int end, int destValue) {
        // 1. 边界判断
        if (null == array) {
            return -1;
        }

        // 2. 终止判断
        if (start > end) {
            return -1;
        }

        // 3. 递归
        int middle = (start + end) / 2;
        // a. 找到目标取值
        if (array[middle] == destValue) {
            return middle;
        }

        // b. 判断循环数组的左右
        if (array[middle] > array[start]) {// 左边有序
            if (array[middle] > destValue && destValue >= array[start]) {
                return binarySearch(array, start, middle - 1, destValue);
            } else {
                return binarySearch(array, middle + 1, end, destValue);
            }
        } else { // 右边有序
            if (array[middle] < destValue && destValue <= array[end]) {
                return binarySearch(array, middle + 1, end, destValue);
            } else {
                return binarySearch(array, start, middle - 1, destValue);
            }
        }

    }



## 2. 旋转数组中, 查询最小值

思路:

* 递归: 把问题, 化解为子问题, 但是, 需要考虑边界条件。


具体示例代码:

    /**
     * 从有序的旋转数组中, 找出最小值的下标.
     *
     * @param array 有序的旋转数组。
     * @return 最小值对应的下标
     */
    public static int findMinValue(int[] array) {
        // 1. 边界判断
        if (null == array) {
            return -1;
        }

        return binaryFindMinValue(array, 0, array.length - 1);
    }


    /**
     * 递归: 把问题, 化解为子问题, 但是, 需要考虑边界条件。
     *
     * @param array 有序的旋转数组
     * @param start 起始下标
     * @param end 结束下标
     * @return 最小取值的下标
     */
    public static int binaryFindMinValue(int[] array, int start, int end) {
        // 1. 边界判断
        if (null == array) {
            return -1;
        }
        if (start > end) {
            return -1;
        }

        // 2. 终止条件
        if (start == end) {
            return start;
        }
        // 原始的升序数组
        if (array[start] < array[end]) {
            return start;
        }

        // 2. 迭代
        int middle = (start + end) / 2;
        if (array[start] <= array[middle]) {
            // 特列: 取值完全相同
            if (array[start] == array[middle] && array[end] == array[middle]) {
                return getMinIndex(array, start, end);
            }

            // 左边升序, 最小值在右侧
            return binaryFindMinValue(array, middle + 1, end);
        } else {
            // 右侧升序, 最小值在左侧
            return binaryFindMinValue(array, start, middle);
        }

    }

    public static int getMinIndex(int[] array, int start, int end) {
        int minValue = array[start];
        int minIndex = start;
        for (int i = start; i <= end; i++) {
            if (array[i] < minValue) {
                minValue = array[i];
                minIndex = i;
            }
        }
        return minIndex;
    }



## 参考来源


* [旋转数组的二分查找][旋转数组的二分查找]






[NingG]:    http://ningg.github.com  "NingG"

[旋转数组的二分查找]:		http://blog.csdn.net/lclansefengbao/article/details/37591609
