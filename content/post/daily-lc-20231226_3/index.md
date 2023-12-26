---
title: Daily Leetcode - 54. Spiral Matrix
description: Medium 螺旋矩陣
date: 2023-12-26 12:00:00+0000
categories:
    - LeetCode
    - Array
---

##  2023 Dec LC challenge

### 題目 54. Spiral Matrix

[代碼隨想錄-螺旋矩陣](https://www.programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html#%E6%80%9D%E8%B7%AF)
[賈考博-leetcode 54](https://www.youtube.com/watch?v=mmQfavfpW_M)
螺旋矩陣 : 注意邊界問題

* 此題有課能為不對稱矩陣，需多加判斷，避免重複計算
* 遍歷一行少一行，遍歷一列少一列，因為行列都有改變所以要多加判斷是否會重複遍歷

### My Code

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        if (matrix.length == 0 || matrix[0].length == 0) {
            return result;
        }
        int m = matrix.length; //row
        int n = matrix[0].length; //col
        int endRow = m - 1;
        int endCol = n - 1;
        int startx = 0; //(x, y)
        int starty = 0; //(x, y)
        int i;

        while(startx <= endRow && starty <= endCol) {
            for(i = starty; i <= endCol; i++) {
                result.add(matrix[startx][i]);
            }
            startx++;
            
            for(i = startx; i <= endRow; i++) {
                result.add(matrix[i][endCol]);
            }
            endCol--;
            if(startx <= endRow){
                for(i = endCol; i >= starty; i--) {
                    result.add(matrix[endRow][i]);
                }
                endRow--;
            }

            if(starty <= endCol){ //判斷 因為我們上面startx++;做了更動，沒檔可能又跑進來
                for(i = endRow; i >= startx; i--) {
                    result.add(matrix[i][starty]);
                }
                starty++;
            }

        } 
        return result;
    }
}
```