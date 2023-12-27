---
title: Daily Leetcode - 1578. Minimum Time to Make Rope Colorful
description: Medium 用two pointer 解
date: 2023-12-27 12:00:00+0000
categories:
    - LeetCode
    - Dynamic Programming
    - Two Pointer
---

##  2023 Dec LC challenge

### 題目 1578. Minimum Time to Make Rope Colorful

選擇保留移除時間最長的氣球的原因是為了最小化總的移除時間。 這個選擇是基於以下邏輯：

目標是減少連續的同色氣球：為了讓氣球繩多彩，需要確保沒有兩個連續的氣球是同一色。 
代表在一串連續的同色氣球中，我們至少需要移除一個氣球。

* 最小化移除時間：我們的目標是在達到上述條件的同時，使總的移除時間盡可能小。

* 決定保留哪個氣球：在一組連續的同色氣球中，如果我們選擇移除那個需要最長時間來移除的氣球，那麼我們實際上是在選擇最不經濟的選項。 換句話說，移除其他任何一個氣球的成本都會比移除這個最耗時的氣球小。

* 保留最耗時的氣球：因此，最優策略是保留那個需要最長時間來移除的氣球，並移除其他所有同色氣球。 這樣，我們移除氣球的總時間就是這組同色氣球中所有移除時間之和減去最長的那個移除時間。

### My Code

```java
class Solution {
    public int minCost(String colors, int[] neededTime) {
        int left = 0;
        int right = 0;
        int totalTime = 0;
        char[] c = colors.toCharArray();
        while(right < c.length) {
            int currentGroupTime = 0;  // 當前兩個重複顏色要移除的時間總和
            int maxTimeInGroup = 0; // 兩個重複顏色移除時間的最大值

            while(right < c.length && c[right] == c[left]) {
                currentGroupTime += neededTime[right];
                maxTimeInGroup = Math.max(neededTime[right], maxTimeInGroup);
                right++;
            }
            totalTime += currentGroupTime - maxTimeInGroup; // 總和 - - 最大值 = 最小那個
            left = right;
        }
        return totalTime;
    }
}
```

#### 說明

* 內部循環是如何運作的：

初始狀態：一開始，left 和 right 都指向第一個字元 'a'（索引 0）。 此時，currentGroupTime 和 maxTimeInGroup 都初始化為 0。

* 內部循環的開始：

進入內部循環時，right 指向索引 0（第一個 'a'）。 因為 c[right]（即 'a'）和 c[left]（同樣是 'a'）是相同的，所以循環繼續。
currentGroupTime 更新為 neededTime[0]，即 time1。
maxTimeInGroup 更新為 neededTime[0] 和 maxTimeInGroup 中的較大值，這時就是 time1。
然後 right 自增，現在指向索引 1（第二個 'a'）。
內部循環的第二次迭代：

此時，right 指向第二個 'a'，並且因為它仍與 left 指向的 'a' 相同，循環繼續。
currentGroupTime 現在加上 neededTime[1]，即 time1 + time2。
maxTimeInGroup 更新為 neededTime[1] 和目前 maxTimeInGroup 中的較大值，即 max(time1, time2)。
right 再次自增，現在超出了字串的範圍，循環結束。

* 內部循環結束：

此時，我們已經處理了一組連續的同色氣球'aa'，併計算出了它們的總移除時間currentGroupTime（time1 + time2）和這組中最大的單一移除時間maxTimeInGroup（max(time1, time2 )）。
在外部循環中，我們計算 totalTime 為 currentGroupTime - maxTimeInGroup，即 (time1 + time2) - max(time1, time2)。 這代表了除了最難移除的氣球以外其他氣球的移除時間。
透過這個過程，currentGroupTime 成功地累積了一組連續同色氣球的總移除時間，而 maxTimeInGroup 則確保我們只保留了這組中移除成本最高的氣球。