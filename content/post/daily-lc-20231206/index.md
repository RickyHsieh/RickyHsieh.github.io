---
title: Daily Leetcode - 1716. Calculate Money in Leetcode Bank
description: 2023 Dec LC challenge Day 6
date: 2023-12-07 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

#### 1716. Calculate Money in Leetcode Bank

今天是第六天，題目是 Easy 級，看出規律後就可以解了，用了兩種方法。
迭代iteration和遞迴recursion。

## My Code

Hercy wants to save money for his first car. He puts money in the Leetcode bank every day.
He starts by putting in $1 on Monday, the first day. Every day from Tuesday to Sunday, he will put in $1 more than the day before. On every subsequent Monday, he will put in $1 more than the previous Monday.
Given n, return the total amount of money he will have in the Leetcode bank at the end of the nth day.

### Iteration

#### case 1 計算完整星期的存款：

計算完整星期數 weeks = n / 7。

使用 for 迴圈遍歷每個完整的星期。 對於每個星期，計算總存款，初始為 $28（1週的存款），然後根據星期數增加額外的金額（每過一周，每天的存款都會增加 $1）。
這裡，28 + 7 * (week - 1) 表示每週的累積存款金額。

因為
| 周次 | 星期一 | 星期二 | 星期三 | 星期四 | 星期五 | 星期六 | 星期日 | 累計 |
|------|--------|--------|--------|--------|--------|--------|--------|------------|
| 第1周 | $1     | $2     | $3     | $4     | $5     | $6     | $7     | $28        |
| 第2周 | $2     | $3     | $4     | $5     | $6     | $7     | $8     | $35        |
| 第3周 | $3     | $4     | $5     | $6     | $7     | $8     | $9     | $42        |


可以看出

* 每周差額為 7 (等差)，代表每一天為上一周 + 1

* 以每周一比較，可以發現

| 周次   | 星期一的存款 | 周累計存款公式          |
|--------|--------------|------------------------|
| 第1周  | $1 + 0       | 28 + 7 * (1 - 1) = $28 |
| 第2周  | $1 + 1       | 28 + 7 * (2 - 1) = $35 |
| 第3周  | $1 + 2       | 28 + 7 * (3 - 1) = $42 |
| ...    | ...          | ...                    |
| 第n周  | $1 + (n - 1) | 28 + 7 * (n - 1)       |

* 總額 : 28 + 7 * (week - 1)

#### case 2 計算剩餘天數的存款：

計算剩餘的天數 remain = n % 7。
再次使用 for 迴圈遍歷剩餘的每一天，累加每天的存款額。 每天的存款金額由當前週數（weeks）和天數（i）決定。
返回總存款：

最後回傳 total，即累積的存款總額。 

```java
class Solution {
    public int totalMoney(int n) {
        
      int weeks = n / 7;
      int total = 0;
      int remain = n % 7;

      for (int week = 1; week <= weeks; week++) {
          total += 28 + 7 * (week - 1);  
      }

      for (int i = 1; i <= remain; i++) {
        total += i + weeks;
      }

      return total;
    }
}
```

### Recursion

[進入遞迴-recursion-的世界](https://medium.com/appworks-school/%E9%80%B2%E5%85%A5%E9%81%9E%E8%BF%B4-recursion-%E7%9A%84%E4%B8%96%E7%95%8C-%E4%B8%80-59fa4b394ef6)
遞迴思考模式 
`
先將一個大問題，拆解成幾個較小的問題
每個較小的問題，又能依照相同方式拆成更小的問題
每當小問題解決時，大問題也可以依靠小問題的結果來解決
每層的解決方法都是一樣的，除了最小的問題以外
根據以上幾點，我們可以不斷套用相同的函數，讓他自己幫自己解決問題
以上就是遞迴的基本核心精神
`
* 大問題：計算連續 n 天的存款總額。

* 拆解為更小的問題：

    計算連續 n-1 天的存款總額，然後加上第 n 天的存款。
    第 n 天的存款金額取決於已經過去的完整週數以及當前週的天數。

* 再次拆解：

    每週的存款金額比上一周多 $7（每天比對應的前一周同一天多 $1）。
    每天的存款金額是當天在周中的順序（1 到 7），再加上過去的完整週數（從第 0 週開始計數）。

* 最小問題和基礎情況：

    當 n = 0 時，沒有存款，總額為 0。

* 遞迴解決：

    使用遞歸函數計算 n-1 天的存款總額，然後將第 n 天的存款加到這個總額上。
    每次遞歸呼叫都在減少 n 的值，直到達到基礎情況（n = 0）。

#### 一些眉角

```java
int weeks = (n - 1) / 7; 
```
這個表達式中使用 n - 1 是為了正確地計算截至第 n 天所經過的完整星期數。 
這裡的 n - 1 是基於如何計數星期的方式而決定的。

舉例來說: 
假設第一天（即 n = 1）是第一週的第一天。因此，第一週的天數是從 n = 1 到 n = 7。 如果直接使用 n / 7 來計算週數，那麼在 n = 7 時，我們會得到 7 / 7 = 1，表示已經過去了一周，並且是第二週的第一天。 但實際上，第七天仍然屬於第一週。

簡單來說，n - 1 是為了將星期的計數與天數對齊，確保每週的天數計算從0開始，正確反映過去的完整週數。

* n = 7，int weeks = ( 7 - 1) / 7，結果 weeks = 0
* n = 10，int weeks = ( 10 - 1) / 7，結果 weeks = 1 
* n = 14，int weeks = ( 14 - 1) / 7，結果 weeks = 1 仍然在以第一周
* n = 16，int weeks = ( 16 - 1) / 7，結果 weeks = 2


```java
class Solution {
    public int totalMoney(int n) {
       
      if (n == 0) {
        
        return 0;

      } else {

          int week = (n - 1) / 7;
          int dayOfWeek = (n - 1) % 7;
          int total = week + dayOfWeek + 1;
          return totalMoney(n - 1) + total;

      }

    }
}
```
