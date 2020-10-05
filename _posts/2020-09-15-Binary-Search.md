---
layout:     post
title:      Binary search mode
subtitle:   
date:       2020-09-15
author:     Borong
header-img: img/post-bg-github-cup.jpg
catalog: true
tags:
    - Leetcode
    - Binary search
    - Array
---


## Overview

Binary search, also known as half-interval search, logarithmic search, or binary chop, is a search algorithm that finds the position of a target value within a sorted array. Binary search compares the target value to the middle element of the array.[(Wiki)](https://en.wikipedia.org/wiki/Binary_search_algorithm)

### Find the first index of number greater than the target one.

```java
public static int bs1(int[] nums, int t) {
        int l = 0, r = nums.length - 1, mid = 0;
        while (l <= r) {
            mid = l + (r - l) / 2;
            if (nums[mid] <= t)
                l = mid + 1;
            else
                r = mid - 1;
        }
        return l;
    }
```

### Find the first index of number greater than the target one.

```java
public static int bs1(int[] nums, int t) {
        int l = 0, r = nums.length - 1, mid = 0;
        while (l <= r) {
            mid = l + (r - l) / 2;
            if (nums[mid] <= t)
                l = mid + 1;
            else
                r = mid - 1;
        }
        return r;
    }
```
*Time complexity:* O(log2^n): if the length of an array is n, the number of searching is X, so 2^X = n, then X = log2^n

*Space complexity:* O(1)