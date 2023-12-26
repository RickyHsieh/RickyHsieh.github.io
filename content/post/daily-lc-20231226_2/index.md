---
title: Daily Leetcode - 59. Spiral Matrix II
description: Medium 螺旋矩陣2
date: 2023-12-26 12:00:00+0000
categories:
    - LeetCode
    - Array
---

##  2023 Dec LC challenge

### 題目 59. Spiral Matrix II

[代碼隨想錄-螺旋矩陣](https://www.programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html#%E6%80%9D%E8%B7%AF)
螺旋矩陣 : 注意邊界問題

* 左閉右開 (本題用這個)
* 左閉右閉
* 那如果要循環? 要轉幾圈? 題目給 n ，假設 n = 4 ，每轉一圈少兩行所以 n / 2 = 2
    (另一個說法)
* 方陣


### My Code

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int loop = 0; 
        int[][] res = new int[n][n];
        int start = 0; 
        int count = 1; 
        int i, j;
        while(loop < n / 2) {
             loop++;
            for (j = start; j < n - loop; j++) {
                res[start][j] = count++;
            }

            for (i = start; i < n - loop; i++) {
                res[i][j] = count++;
            }

            for (; j >= loop; j--) {
                res[i][j] = count++;
            }

            for (; i >= loop; i--) {
                res[i][j] = count++;
            }
           
            start++;
        }
        if (n % 2 == 1) {
           res[start][start] = count;
        }
        return res;
    }
}
```