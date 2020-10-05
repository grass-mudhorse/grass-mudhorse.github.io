---
layout:     post
title:      Remove a certain element in an Array
subtitle:   
date:       2020-10-05
author:     Borong
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - Leetcode
    - Array
---


## Overview

There are two questions I found related to this solution

### Move Zeroes

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

>Input: [0,1,0,3,12]  
>Output: [1,3,12,0,0]

**Note:**

1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

[(LeetCode)](https://leetcode-cn.com/problems/move-zeroes)

**Solution:**

1. Use *znum* to count the occurrence of zero
2. if nums[i] is not 0, it should move to nums[i - znum].
3. append zeros from the end of the array to nums[len - znum].

*Time complexity:* O(n+k): iterate over the array once and append k zeros to the array.

*Space complexity:* O(1): didn't use extra array.

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int znum = 0, len = nums.length;
        for (int i = 0; i < len; i++) {
            if (nums[i] == 0) {
                ++znum;
            } else {
                nums[i - znum] = nums[i];
            }
        }
        for (int i = len -1; i > len - 1 - znum; --i) {
            nums[i] = 0;
        }
    }
}
```

### Remove Element

Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

>Given nums = [3,2,2,3], val = 3,  
>  
>Your function should return length = 2, with the first two elements of nums being 2.  
>  
>It doesn't matter what you leave beyond the returned length.

**Example 2:**

>Given nums = [0,1,2,2,3,0,4,2], val = 2,  
>  
>Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.  
>  
>Note that the order of those five elements can be arbitrary.  
>  
>It doesn't matter what values are set beyond the returned length.

[(LeetCode)](https://leetcode-cn.com/problems/remove-element)

**Solution:**

1. Use *vnum* to count the occurrence of target *val*.
2. if nums[i] is not *val*, it should move to nums[i - vnum].
3. the new length of the array is *len - vnum*.

*Time complexity:* O(n): iterate over the array once.

*Space complexity:* O(1): didn't use extra array.

```java
class Solution {
   public int removeElement(int[] nums, int val) {
        int vnum = 0, len = nums.length;
        for (int i = 0; i < len; i++) {
            if (nums[i] == val) {
                ++vnum;
            } else {
                nums[i - vnum] = nums[i];
            }
        }
        return len - vnum;
    }
}
```
