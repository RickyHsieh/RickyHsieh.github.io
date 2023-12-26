---
title: Daily Leetcode - 1155.Number of Dice Rolls With Target Sum
description: Medium 動態規劃再找時間補
date: 2023-12-26 12:00:00+0000
categories:
    - LeetCode
    - 二分法
---

##  2023 Dec LC challenge

### 題目 1155.Number of Dice Rolls With Target Sum

這個問題是一個典型的動態規劃問題，其中涉及到計算給定數量的骰子（n 個），每個骰子有k 個面（編號為1 到k），擲出它們時面朝上的數字之和 等於一個特定目標值（target）的可能方式的數量。

要解決這個問題，我們可以使用動態規劃的方法。 這種方法涉及建立一個二維數組（或等價的資料結構），其中每個元素代表達到特定和的方式的數量。 我們可以逐步建立這個數組，直到達到目標和。

問題解釋
輸入：

n：骰子的數量。
k：每個骰子的面數。
target：我們要達到的目標和。
輸出：

傳回達到目標和 target 的不同方式的數量。
動態規劃邏輯：

建立一個二維數組 dp，其中 dp[i][j] 表示用 i 個骰子組成和為 j 的不同方式的數量。
初始化 dp[0][0] = 1，因為用 0 個骰子組成和為 0 的方式只有一種，就是什麼都不做。
遍歷每個骰子（1 到 n），對於每個骰子，更新和的可能性。 對於每個可能的和（1 到 target），考慮所有可能的骰子麵值（1 到 k）。
對於每個骰子面值，更新 dp[i][j]。 如果目前和 j 大於或等於骰麵值，那麼 dp[i][j] += dp[i-1][j - 骰麵值]。
模運算：

由於答案可能非常大，所以需要對結果進行模運算（10^9 + 7）。
演算法範例
假設 n = 2（2 個骰子），k = 6（每個骰子有 6 個面），target = 7（目標和為 7）。 我們需要計算使用這兩個骰子組成和為 7 的不同方式的數量。

### My Code

這題目的，用於計算達到目標和的不同方式數量。它接收三個參數：n（骰子的數量），k（每個骰子的面數），和 target（目標和）。

```java
public class Solution {
    public int numRollsToTarget(int n, int k, int target) {
```

我們定義一個數組，
```java
long[][] dp = new long[n+1][target+1];
```
定義一個2D數組 dp，其中 dp[i][j] 表示用 i 個骰子得到總和為 j 的方式數量。使用 long 類型是為了防止在計算過程中出現整數溢出。

```java
dp[0][0] = 1
```
初始化 dp[0][0] 為 1，意味著没有骰子（i = 0）且目標和為 0（j = 0）的情况只有一種可能，即不擲任何骰子。

```java
for(int i = 1; i < n + 1; i++){
```
最外層循環，遍歷每一面骰子。

```java
    for(int j = 1; j < target + 1; j++){
```
遍歷 1 到 target 所有可能總和。

```java
                long sum = 0;
                for(int x = 1; x < k+1; x++){
```
對於每个 i 和 j 的組合，初始化一个 sum 來累加所有可能達到總和 j 的方式數量。内部的循环遍歷所有可能的骰子面值

```java
                    if(j-x >= 0){sum += dp[i-1][j-x];}
```
如果當前總和 j 減去骰子面值 x 不小於 0，則將 dp[i-1][j-x] 的值累加到 sum 中。這代表了使用前 i-1 個骰子達到總和 j-x 的所有方式。

```java
                }
                dp[i][j] = sum % 1000000007;
```
將累加得到的 sum 對 1000000007 取模後，賦值给 dp[i][j]。這一步是為了防止整數溢出，並滿足題目要求的模運算。

```java
            }
        }
        return (int)(dp[n][target] % 1000000007);
    }
}

```

返回使用 n 個骰子達到總和 target 的方式數量，對結果再次進行模運算以確保答案的正確性。

這個方法透過動態規劃計算了使用 n 個骰子達到特定總和的所有可能方式的數量。 它逐步建立起 dp 數組，每個元素都基於前面的計算結果。 這種方法有效地利用了重疊子問題的特性，是解決此類計數問題的經典方法。

#### full code

```java
class Solution {
    public int numRollsToTarget(int n, int k, int target) {
        long[][] dp = new long[n+1][target+1];
        dp[0][0] = 1;
        for(int i = 1; i < n + 1; i++){
            for(int j = 1; j < target + 1; j++){
                long sum = 0;
                for(int x = 1; x < k+1; x++){
                    if(j-x >= 0){sum += dp[i-1][j-x];}
                }
                dp[i][j] = sum % 1000000007;
            }
        }
        return (int)(dp[n][target] % 1000000007);
    }
}

// dp[i][j] = using i dices, number of ways to satisfy j
// dp[i][j] = dp[i-1][j-x] for x from 1 to k 
```