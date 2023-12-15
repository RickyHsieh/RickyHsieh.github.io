---
title: Algorithm sliding window 模板
description: sliding window 模板整理
date: 2023-12-15 14:37:00+0000
categories:
    - Algorithm
---

##  sliding window 模板整理

### Sliding window

概念就是可以使用一個 pointer 以及一個 window size 去實作，且會利用 window 中的 elements去依照情境去使用，就不用像 two pointer 兩個 pointer 去實作。

### 解題模板

滑動視窗（Sliding Window）是一種常用的解決陣列或字串問題的方法，尤其適用於需要找出滿足某種條件的最長或最短子數組/子字串的問題：

#### 模板結構

初始化視窗邊界和所需變數：

初始化兩個指標 left 和 right，分別表示視窗的左右邊界。 一般情況下，兩個指標初始都指向陣列的起始位置。
根據問題需求初始化其他所需的變數（例如用於計數、求和等）。
視窗的擴展（右移右指針）：

增加 right 指針，擴大窗口，直到視窗內的子數組/子字串滿足特定條件。
每次移動右指標後，根據需要更新所需變數的狀態。
視窗的收縮（右移左指針）：

當視窗內的子數組/子字串滿足條件時，逐步右移 left 指標以收縮窗口，直到視窗不再滿足條件。
每次移動左指標後，同樣更新所需變數的狀態。
更新所需的結果：

在每次視窗改變（擴展或收縮）時，根據題目要求更新結果。
重複以上步驟直到結束：

繼續移動右指標直到陣列/字串的結尾，重複上述過程。

```java
public int slidingWindowTemplate(int[] nums) {
     int left = 0, right = 0;
     int result = 0; // 根據具體問題調整
     // 可能需要的其他變數初始化

     while (right < nums.length) {
         // 根據視窗內的資料更新狀態
         // ...

         while (/* 視窗內的子數組滿足特定條件 */) {
             // 更新所需的結果
             // ...

             // 移動左指針，縮小視窗
             // 更新視窗狀態
             left++;
         }

         // 擴充視窗
         right++;
     }
     return result;
}
```