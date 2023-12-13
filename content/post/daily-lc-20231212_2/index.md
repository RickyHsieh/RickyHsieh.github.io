---
title: Daily Leetcode - 1582. Special Positions in a Binary Matrix
description: Easy 
date: 2023-12-12 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 2390. Removing Stars From a String

Given an m x n binary matrix mat, return the number of special positions in mat.

A position (i, j) is called special if mat[i][j] == 1 and all other elements in row i and column j are 0 (rows and columns are 0-indexed).

[1][0][0]
[0][0][1]
[1][0][0]

Input: mat = [[1,0,0],[0,0,1],[1,0,0]]
Output: 1

### My Code

### 解法一

```java
class Solution {
    public int numSpecial(int[][] mat) {
        int specialCount = 0;
        int[] rowSum = new int[mat.length];
        int[] colSum = new int[mat[0].length];

        for (int i = 0; i < mat.length; i++) {
            for (int j = 0; j < mat[i].length; j++) {
                rowSum[i] += mat[i][j];
                colSum[j] += mat[i][j];
            }
        }

        for (int i = 0; i < mat.length; i++) {
            for (int j = 0; j < mat.length; j++) {
                if (mat[i][j] == 1 && rowSum[i] == 1 && colSum[j] == 1) {
                    specialCount++;
                }
            }
        }
        return specialCount;
    }
}
```


#### 遇到的問題
`java.lang.ArrayIndexOutOfBoundsException: Index 2 out of bounds for length 2
  at line 16, Solution.numSpecial
  at line 54, __DriverSolution__.__helper__
  at line 84, __Driver__.main`

具體的例子來說明 ArrayIndexOutOfBoundsException 的原因和如何避免它。
假設我們有一個非正方形的二維數組（矩陣）mat，例如：
```java
int[][] mat = {
    {1, 0, 0},
    {0, 1}
};
```
這個矩陣有兩行，但第一行有3個元素，第二行只有2個元素。 如果我們使用 mat[0].length（即第一行的長度）作為內層循環的界限，我們的程式碼可能看起來像這樣：

```java
for (int i = 0; i < mat.length; i++) {
     for (int j = 0; j < mat[0].length; j++) { // 以第一行的長度為界限
         // 存取 mat[i][j]
     }
}
```

#### 時間複雜度：
O(m×n)+O(m×n)=O(m×n)

#### 空間複雜度
儘管增加了兩個額外的數組（每行和每列的1的計數），但這些數組的大小分別是 m 和 n，所以空間複雜度是 O(m+n)。 當矩陣的大小相對較小時。