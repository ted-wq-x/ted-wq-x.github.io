---
title: Binary Search
description: 二分查找4种区间形式
pubDatetime: 2025-09-02T07:04:09.619Z
author: WQ
slug: binary-search
tags:
    - 算法
---

说来惭愧，写代码多年，到今天才知道二分查找存在4种区间形式，这里记录下。

## Table of contents

区间确定了
1. while处的循环判断条件
2. right&left更新值是否需要+/-1

## 左闭右闭

```java
int binarySearch(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    //因为都是闭区间，所有left可以等于right
    while (left <= right) {
        int mid = left + (right - left) / 2;
        //对于更新left&right，因为mid不是最终的结果，且是闭区间，所以都需要+/-1
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return -1;
}
```

## 左开右闭

```java
int binarySearch(int[] nums, int target) {
    int left = -1, right = nums.length - 1;
    while (left < right) {
        //特别的，int mid = left + (right - left) / 2;是向下取整的
        //因为左侧取的mid，如果mid是向下取整的，就会导致left一直等于mid，死循环
        //所以需要采用向上取整的方式
        int mid = left + (right - left + 1) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else {
            left = mid;
        }
    }
    return -1;
}
```

## 左闭右开

```java
int binarySearch(int[] nums, int target) {
    int left = 0, right = nums.length;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] > target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return -1;
}
```

## 左开右开

```java
int binarySearch(int[] nums, int target) {
    int left = -1, right = nums.length;
    while (left + 1 < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] > target) {
            right = mid;
        } else {
            left = mid;
        }
    }
    return -1;
}
```