---
title: HackerRank - Mini-Max Sum
description: 
date: 2023-11-27 00:00:00+0000
image: hk-cover1.jpg
categories:
    - HackerRank
tags:
    - HackerRank
---

## HackerRank - Mini-Max Sum

Given five positive integers, find the minimum and maximum values that can be calculated by summing exactly four of the five integers. Then print the respective minimum and maximum values as a single line of two space-separated long integers.

Example
arr = [1, 3, 5, 7, 9]
The minimum sum is 1+3+5+7=16 and the maximum sum is 3+5+7+9=24 . The function prints
```
16 24
```

## My code

### 修正前
一開始的想法，沒考慮到array中有可能有負數的作法 : 
```java
    public static void miniMaxSum(List<Integer> arr) {
    // Write your code here
        
        List<Integer> list = new ArrayList<>();
        int sum = 0;
        int min = 0;
        
        for (int value : arr) {
            sum += value;
        }
        
        min = sum;
        int max = 0;
        for (int value : arr) {
            int sumWithoutValue = sum - value;
               
            if( sumWithoutValue > max) {
                max = sumWithoutValue;
            }
            
            if( sumWithoutValue < min) {
                min = sumWithoutValue;
            }
        }   
        System.out.println(min + " " + max);
        
    }


```
* 新增一個總和變數
* 先加總整個List
* 給予兩個變數 min max
* 先將總和賦值給變數 min
  目的: 排除一個元素後的總和必定小於或等於所有元素的總和（因為所有元素都是正數）。因此，通過將 min 初始設置為 sum，我們可以確保在遍歷陣列時，任何比 sum 小的總和都會更新 min。

* 接下來邏輯的部分就是 : 
  逐一排除元素後的總和 : sumWithoutValue
    - 如果 sumWithoutValue 大於 max，max 為 sumWithoutValue
    - 如果 sumWithoutValue 小於 min，min 為 sumWithoutValue


## 修正後

* 考量溢出問題用 Long
* 以及負數

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

class Result {

    /*
     * Complete the 'miniMaxSum' function below.
     *
     * The function accepts INTEGER_ARRAY arr as parameter.
     */

    public static void miniMaxSum(List<Integer> arr) {
    // Write your code here
        
        long totalSum = 0;
        long minSum = Long.MAX_VALUE;
        long maxSum = Long.MIN_VALUE;

        for (int value : arr) {
            totalSum += value;
        }

        for (int value : arr) {
            long sumWithoutValue = totalSum - value;
            minSum = Math.min(minSum, sumWithoutValue);
            maxSum = Math.max(maxSum, sumWithoutValue);
        }

        System.out.println(minSum + " " + maxSum);
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        List<Integer> arr = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        Result.miniMaxSum(arr);

        bufferedReader.close();
    }
}

```