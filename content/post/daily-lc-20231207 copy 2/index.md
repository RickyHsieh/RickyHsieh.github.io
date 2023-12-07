---
title: Daily Leetcode 42. Trapping Rain Water
description: Hard難度，使用Two Pointer
date: 2023-12-07 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

### 42. Trapping Rain Water

題目是 Hard 級。
題目大意: 能困住最多的雨水總量。


### 想法

Hi，我使用 Two Pointers，一開始先初始化兩個指標 L 和 R，分別指向陣列的開始和結束。

為了計算積水量，需要追蹤左側和右側的最高長條，所以分別為設定了 leftMax 和 rightMax。 這兩個變數在每次迭代中更新，確保 leftMax 和 rightMax 分別是左側和右側遇到的最高長條的高度。

在遍歷過程中，我比較 L 和 R 處的高度。 如果 L 處的高度小於 R 處，這表示 L 處可能有積水，所以我更新 leftMax 並計算該位置的積水量。 同理，如果 R 處的高度小於或等於 L 處，我會去更新 rightMax 並計算該位置的積水。

這個過程一直持續到 L 和 R 相遇，最後累積的積水量就是整體的雨水量~~


### 雙指針初始化：
初始化兩個指標 L 和 R，分別指向陣列的開始和結束位置。

### 雨水累積的條件：
雨水的累積取決於每個位置左右兩側的最高長條圖，具體而言，是左右兩側的「最短」最高長條。

### leftMax 和 rightMax 的角色：
leftMax 和 rightMax 用於儲存左側和右側遍歷過程中遇到的最高長條的高度。 這兩個變數可以幫助確定每個位置能夠累積多少雨水。

### 比較 L 和 R 的高度：
如果 L 處的高度小於 R 處的高度，那麼 L 處有潛在的雨水累積空間。 此時應更新 leftMax 並計算可能的積水量。 反之，若 R 處的高度小於或等於 L 處的高度，應更新 rightMax 並計算右側可能的積水量。

### 計算積水量：
如果 leftMax 大於目前 L 處的高度，積水量為 leftMax - height[L]。 同理，如果 rightMax 大於目前 R 處的高度，積水量為 rightMax - height[R]。

### 移動指針和累積總雨水量：
在處理完目前位置後，對應的指標（L 或 R）需要向中間移動。
同時，每次計算出的積水量應會累積到總雨水量中。



### My Code

```java
class Solution {
    public int trap(int[] height) {

        int left = 0; 
        int right = height.length - 1;
        int leftMax = height[0];
        int rightMax = height[height.length - 1];
        int total = 0;

        while( left < right) {

            if (height[left] < height[right]) {
                
                leftMax = Math.max(leftMax,height[left]);

                if (leftMax > height[left]) {
                    total += leftMax - height[left];
                }
                left++;

            } else {
                
                rightMax = Math.max(rightMax, height[right]);

                 if (rightMax > height[right]) {
                    total += rightMax - height[right];
                }
                right--;
            }
            
        }
        return total;
    }
}
```
#### Complexity
* Time complexity:O(n)，其中 n 是陣列 height 的長度。

* Space complexity: O(1)

