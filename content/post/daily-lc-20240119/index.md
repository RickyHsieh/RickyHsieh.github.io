---
title: Daily Leetcode - 931. Minimum Falling Path Sum
description: Medium
date: 2024-01-19 12:00:00+0000
categories:
    - DynamicProgramming
---

##  2024 Jan LC challenge

### 題目  459. Repeated Substring Pattern

* 方形矩陣：輸入是一個 n x n 的整數數組，這裡的 n 表示矩陣的行數和列數。

* 下降路徑：下降路徑是指從矩陣的第一行開始，逐行向下選擇元素的路徑。 在每一步，你都會從目前行移動到下一行。

* 路徑選擇規則：對於矩陣中的任何一個位於 (row, col) 位置的元素，你在下一行可以選擇移動到：

正下方的元素 (row + 1, col)
左下方的對角元素 (row + 1, col - 1)
右下方的對角元素 (row + 1, col + 1)
這些規則確保路徑可以透過矩陣向下移動，可以直接向下或斜向下移動。

目標：目標是找到一條從最上方一行到最下方一行的路徑，使得該路徑上的元素總和最小。

這個問題是一個典型的動態規劃問題，其中問題的最適解依賴其子問題的最適解。 解決方法大致如下：

* 基礎情況：對於第一行，每個元素的「最小」路徑和就是該元素本身的值，因為第一行上面沒有其他元素。

* 遞歸關係：從第二行到最後一行，你可以透過考慮到達上一行中直上方、左上方對角線和右上方對角線三個可能前置元素的最小路徑和，再加上目前元素的值， 來計算到每個元素的最小路徑和。

* 邊緣情況：在考慮對角線移動時，要小心矩陣的邊緣。 對於第一列和最後一列，其中一個對角線將會超出矩陣範圍。

* 最終結果：最小下降路徑和將是在計算了所有路徑後，最後一行中找到的最小值。

用程式碼實現這個邏輯涉及遍歷矩陣並根據上述規則更新每個單元格的和，以此來找出到達該單元格的最小路徑和。


### My code 

### 方法一

```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int n = matrix.length;
        int[][] dp = new int[n][n]; 

        // first row initializ
        for(int j = 0; j < n; j++) {
            dp[0][j] = matrix[0][j];
        }

        // counting shortest path from others, starting from second row. so i = 1 
        for(int i = 1; i < n; i++) {
            for(int j = 0; j < n; j++) {

                // 當前(row, col) 正上方為 (row - 1, col)
               int min = dp[i - 1][j];

                // 當前位置(左下斜)，往右上斜找(row - 1, col + 1)
                // 必須不在最後一個col
                if(j < n - 1) {
                    min = Math.min(min, dp[i - 1][j + 1]);
                }

                // 當前位置(右斜下)，往左上斜找 (row - 1, col - 1)
                if(j > 0) {
                    min = Math.min(min, dp[i - 1][j - 1]);
                }

                dp[i][j] = min + matrix[i][j];
            }
        }

        int minPathSum = dp[n - 1][0];// dp最後一行第一個元素;
        for(int j = 0; j < n; j++) {
            minPathSum = Math.min(minPathSum, dp[n-1][j]);
        }

        return minPathSum;
    }
}
```
