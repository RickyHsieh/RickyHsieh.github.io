---
title: Daily Leetcode 867. Transpose Matrix
description: Easy 轉置矩陣
date: 2023-12-10 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

今天在上大提琴課前坐在711刷，好險今天題目EZ。

### 題目

就是轉置矩陣，
這題比較容易，
今天又是禮拜天，
肯定要快樂水一篇。

Given a 2D integer array matrix, return the transpose of matrix.

The transpose of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

### My Code

```java
class Solution {
    public int[][] transpose(int[][] matrix) {
       int row = matrix.length;
       int col = matrix[0].length;
       int[][] arr = new int[col][row];
       for(int i = 0; i < col; i++){
           for(int j = 0; j < row; j++){
               arr[i][j] = matrix[j][i];
           }
       }
       return arr;
    }  
}
```