---
title: Daily Leetcode - 2352 equal row and column pairs
description: Medium Hashmap
date: 2023-12-18 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 2352 equal row and column pairs

Given a 0-indexed n x n integer matrix grid, return the number of pairs (ri, cj) such that row ri and column cj are equal.

A row and column pair is considered equal if they contain the same elements in the same order (i.e., an equal array).

### My Code


使用map，
先找出每一Row 的值，用 StringBuilder 製成 rowMap 的 key。 

```java
class Solution {
    public int equalPairs(int[][] grid) {

        int n = grid.length; //方陣
        Map<String, Integer> rowMap = new HashMap<>();
        int pair = 0;

        for (int i = 0; i < n; i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < n; j++) {
                sb.append(grid[i][j]).append(",");
            }
            rowMap.put(sb.toString(), rowMap.getOrDefault(sb.toString(), 0) + 1);
        }

         for (int j = 0; j < n; j++) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < n; i++) {
                sb.append(grid[i][j]).append(",");
            }
            pair += rowMap.getOrDefault(sb.toString(), 0);
        }

        return pair;

    }
}
```

#### 法二 : 使用轉置矩陣

```java
class Solution {
    public int equalPairs(int[][] grid) {
        int pair = 0;
        int[][] rowSet = grid; // row 就原本的 row
        int[][] colSet = new int[grid.length][grid[0].length];

        //轉置矩陣
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++){
                colSet[j][i] = grid[i][j];
            }
        }
        //比較兩個矩陣
        for (int i = 0; i < rowSet.length; i++) {
            for (int j = 0; j < colSet.length; j++) {
                if (Arrays.equals(rowSet[i], colSet[j])) {
                    pair++;
                }
            }
        }
        return pair;
    }
}
```

轉置舉例:

```java
grid = [[1, 2, 3],
        [2, 3, 4],
        [3, 4, 5]]

```
轉置grid獲得 : 
```java
colSet = [[1, 2, 3],
          [2, 3, 4],
          [3, 4, 5]]
```
rowSet(原grid) 與 colSet做比較。 
