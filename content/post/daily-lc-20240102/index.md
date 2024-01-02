---
title: Daily Leetcode - 2610. Convert an Array Into a 2D Array With Conditions
description: Medium 製作一個2D Array
date: 2024-01-02 12:00:00+0000
categories:
    - LeetCode
    - Hash Table
---

##  2024 Jan LC challenge

### 題目  2610. Convert an Array Into a 2D Array With Conditions

將一個1D陣列，轉換成 2D 陣列，並滿足以下條件。

* The 2D array should contain only the elements of the array nums.
* Each row in the 2D array contains distinct integers.
* The number of rows in the 2D array should be minimal.

### 方法

* 計算1D陣列，元素出現次數
* 找出最大出現次數，這個就代表我需要有多少Rows
* 建造一個新2D array
* 遍歷原數組，塞入新陣列中(要先判斷是否重複)

### My Code

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n;
        int fast = getNext(n);
        do {
            slow = getNext(slow);
            fast = getNext(getNext(fast));
        } while(fast != 1 && fast != slow);
        return fast == 1;
    }

    private int getNext(int number) {
        int totalSum = 0;
        while (number > 0) {
            int d = number % 10;
            number = number / 10;
            totalSum += d * d;
        }
        return totalSum;
    }
}
```
