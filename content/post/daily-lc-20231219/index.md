---
title: Daily Leetcode - 661. Image Smoother
description: Easy 矩陣題目還是要加強下 QQ 
date: 2023-12-19 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 661. Image Smoother

An image smoother is a filter of the size 3 x 3 that can be applied to each cell of an image by rounding down the average of the cell and the eight surrounding cells (i.e., the average of the nine cells in the blue smoother). If one or more of the surrounding cells of a cell is not present, we do not consider it in the average (i.e., the average of the four cells in the red smoother).

### My Code


#### 方法一
```java
class Solution {
    public int[][] imageSmoother(int[][] img) {
        
        int rowNums = img.length;
        int colNums = img[0].length;
        int[][] result = new int[rowNums][colNums];

        for (int i = 0; i < rowNums; i++) {
            for (int j = 0; j < colNums; j++) {
                
                int count = 0;
                int sum = 0;

                for(int row = i - 1; row <= i + 1; row++) {
                    for(int col = j - 1; col <= j + 1; col++) {
                        if((row >= 0 && row < rowNums) && (col >= 0 && col < colNums)) {
                            sum += img[row][col];
                            count++;
                        }
                    }
                }

                result[i][j] = sum / count;
            }
        }
        return result;
    }
}
```
* int[][] result = new int[rowNums][colNums]; 創建新2D array。

* int numRows = matrix.length;：這一行取得矩陣的行數（numRows）。

* int numCols = matrix[0].length;：這一行取得矩陣的列數（numCols）。

* for (int i = 0; i < numRows; i++) {：這是一個嵌套的for循環，用於遍歷矩陣的行。

* for (int j = 0; j < numCols; j++) {：這是內部的巢狀for循環，用於遍歷矩陣的列。

* int sum = 0;：這一行初始化了一個變數sum，用於儲存元素及其周圍元素的總和。

* int count = 0;：這一行初始化了一個變數count，用來儲存參與平均值計算的元素個數。

* for (int row = i - 1; row <= i + 1; row++) {：這是一個巢狀的for循環，用於遍歷目前元素的周圍行。

* for (int col = j - 1; col <= j + 1; col++) {：這是內部的巢狀for循環，用於遍歷目前元素的周圍列。

* if (row >= 0 && row < numRows && col >= 0 && col < numCols) {：這一行檢查目前行和列是否在矩陣的有效範圍內。

* sum += matrix[row][col];：如果在有效範圍內，將目前元素的值加到sum中。

* count++;：每次參與平均值計算的元素個數加1。

* sum / count;：這一行計算平均值，並將結果儲存於average變數中。

