---
title: Daily Leetcode - 34. Find First and Last Position of Element in Sorted Array
description: Medium 二分法
date: 2023-12-25 12:00:00+0000
categories:
    - LeetCode
    - 二分法
---

##  2023 Dec LC challenge

### 題目 34. Find First and Last Position of Element in Sorted Array

用兩次二分法找target最初位置以及最後一個位置

### My Code

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
       int start = findPosition(nums, target, true);
       if (start == nums.length || nums[start] != target) {
            return new int[]{-1, -1};
        }
       int end = findPosition(nums, target, false)-1;
       //目標值的結束位置的下一個位置」調整回「目標值的實際結束位置。
       return new int[]{start, end};
    }

    public int findPosition(int[] nums, int target, boolean findStart) {
        int left = 0;
        int right = nums.length;
        while(left < right) {
            int mid = left + (right - left)/2;
            if(nums[mid] > target) {
                right = mid;
            } else if(nums[mid] < target) {
                left = mid + 1;
            } else if( findStart && nums[mid] == target) {
                // 找起始位置
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```