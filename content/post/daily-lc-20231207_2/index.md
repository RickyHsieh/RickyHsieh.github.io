---
title: Daily Leetcode -1903. Largest Odd Number in String
description: 2023 Dec LC challenge Day 7 字元型數字轉換為對應的整數數字
date: 2023-12-07 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

#### 1903. Largest Odd Number in String

今天是第7天拉，題目是 Easy 級。
題目大意: 給定一個數字字串，找出最大的奇數(子字串)。

看到這個題目第一個想法是滑動視窗，two pointer，但題目看清楚後才知道只要，注意結尾是否為基數就好，
因此我只需要一個右指標，往前移動，直到0。

需要注意的是，轉型為數字溢出問題(轉換成int 或 long 再做比較，會爆)，因此使用<span style="color:yellow">字元型數字轉換為對應的整數數字。</span>

## My Code


```java
class Solution {
    public String largestOddNumber(String num) {

        int right = num.length() - 1;

        while(right >= 0) {
            
            if ((num.charAt(right)-'0') % 2 != 0) {                
                return num.substring(0, right + 1);
            }

          right--;
        }

        return "";
    }
}
```

#### 字元型數字轉換為對應的整數數字

num.charAt(right) - '0' 原理如：

num.charAt(right)：這部分從字串 num 中取得位於索引為 right 處的字元。 

例如，如果 num 是 "12345"，且 right 是 2，那麼 num.charAt(right) 將會是字元 '3'。

-'0'：

這裡的 '0' 是字元字面量，表示數字 0 的字元。 在 Java 中，每個字元都有一個與之對應的整數 ASCII 值。 例如，字元 '0' 的 ASCII 值是 48，字元 '1' 的 ASCII 值是 49，以此類推，直到字元 '9' 的 ASCII 值是 57。

相減運算：當您從一個字元型數字中減去 '0' 時，實際上是在減去字元 '0' 的 ASCII 值。 這個操作將字元型數字轉換為其實際的整數值。 例如，'3' - '0' 相當於 51 - 48（因為字元 '3' 的 ASCII 值是 51），結果是整數 3。

常用於處理字串中的單一數字字元。