---
title: Daily Leetcode - 189. Rotate Array
description: 反轉陣列 Rotate 多次反轉技巧(額外空間和in-place)
date: 2023-12-22 13:00:00+0000
categories:
    - LeetCode
    - Array
---

##  2023 Dec LC challenge

### 題目 189. Rotate Array
Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

### My Code

#### 方法一

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int len = nums.length;
        int[] result = new int[len];
        k = k % len; 

        for(int i = 0; i < len; i++) {
            result[(i+k) % len] = nums[i];
        }
        
        for(int i = 0; i < len; i++) {
            nums[i] = result[i];
        }
    }
}
```

#### 方法二

假設我們有一個陣列 nums = [1, 2, 3, 4, 5, 6, 7]，我們想要將它向右旋轉 k = 3 次。

* 步驟 1: 調整旋轉次數
  由於陣列長度是 7，我們先將 k 調整為 k % 7，這裡 k 本身是 3，所以不需要調整。

* 步驟 2: 反轉整個陣列
  原始數組：[1, 2, 3, 4, 5, 6, 7]
  反轉後：[7, 6, 5, 4, 3, 2, 1]

* 步驟 3: 反轉前 k 個元素
  只反轉數組的前 3 個元素。
  反轉前 3 個元素後：[5, 6, 7, 4, 3, 2, 1]

* 步驟 4: 反轉剩下的 n - k 個元素
  反轉從索引 3 到陣列末端的元素。
  最終結果：[5, 6, 7, 1, 2, 3, 4]

* 這就是陣列 [1, 2, 3, 4, 5, 6, 7] 向右旋轉 3 次後的結果。

如何工作的？
反轉整個數組：這一步將原來在數組後面的元素移動到前面，但這些元素的相對順序是顛倒的。
反轉前 k 個元素：這一步驟將先前移動到前面的元素恢復到正確的順序。
反轉剩餘元素：最後，將陣列剩餘部分也恢復到正確的順序。
這種方法是一種高效的旋轉數組的技巧，因為它避免了單個元素逐個移動的需要，而是透過幾次數組層級的操作來實現目標。

```java
class Solution {
    public void rotate(int[] nums, int k) {
        // adjusting the value of k accouding to nums size.
        k %= nums.length;
        // reverse entire array.
        reverse(nums, 0, nums.length - 1);
        // reverse first k element.
        reverse(nums, 0, k - 1);
        // reverse last n - k elements.
        reverse(nums, k, nums.length - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```