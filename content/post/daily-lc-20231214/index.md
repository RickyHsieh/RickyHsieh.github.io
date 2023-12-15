---
title: Daily Leetcode - 1004. Max Consecutive Ones III
description: Medium Sliding window
date: 2023-12-15 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 1004. Max Consecutive Ones III

Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

#### Example 1:

Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: [1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

### My Code

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        
        int left = 0;
        int max = 0;
        int zeroCount = 0;

        for (int right = 0; right < nums.length; right++) {
            if(nums[right] == 0) { //右指針遍歷找遇到0 zeroCount++
                zeroCount++;
            }

            while(zeroCount > k) { // 當window中的 0 大於可交換的coda k 就調整window大小(左指標移動)
                if(nums[left] == 0) { // 若左指標遇到0 zeroCount--;
                    zeroCount--;
                }
                left++;
            }
            max = Math.max(max, right - left + 1);
        }
        return max; 
    }
}
```
#### Example

例子: [1,1,0,1,1,1] 和 k = 2，目標是找出在最多翻轉 2 個 0 的情況下連續 1 的最大數量。

##### 初始狀態
* nums = [1,1,0,1,1,1]
* k = 2
* left = 0, right = 0, zeroCount = 0, max = 0

##### 迭代步驟

第一步: right = 0
* nums[right] = 1 → zeroCount 維持不變。
* max = Math.max(0, 0 - 0 + 1) = 1 → max = 1
* right 移動到下一個位置。

第二步: right = 1
* nums[right] = 1 → zeroCount 維持不變。
* max = Math.max(1, 1 - 0 + 1) = 2 → max = 2
* right 移動到下一個位置。

第三步: right = 2
* nums[right] = 0 → zeroCount 增加到 1。
* max = Math.max(2, 2 - 0 + 1) = 3 → max = 3
* right 移動到下一個位置。

第四步: right = 3
* nums[right] = 1 → zeroCount 維持不變。
* max = Math.max(3, 3 - 0 + 1) = 4 → max = 4
* right 移動到下一個位置。

第五步: right = 4
* nums[right] = 1 → zeroCount 維持不變。
* max = Math.max(4, 4 - 0 + 1) = 5 → max = 5
* right 移動到下一個位置。

第六步: right = 5
* nums[right] = 1 → zeroCount 維持不變。
* max = Math.max(5, 5 - 0 + 1) = 6 → max = 6
* right 到達陣列末端。

結果
最大連續 1 的數量是 max = 6。
在這個範例中，由於 k = 2，允許翻轉的 0 的數量不限制視窗的擴展，因此最大連續 1 的數量等於數組的長度。 如果 k 較小或陣列中 0 的數量較多，則視窗大小和最大連續 1 的數量會有所不同。
