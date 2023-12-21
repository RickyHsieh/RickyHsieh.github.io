---
title: Daily Leetcode - 19. Remove Nth Node From End of List
description: LinkedList 刷爆
date: 2023-12-21 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 19. Remove Nth Node From End of List

#### 方法一 : 遍歷方式
給你一個LL以及一個n，我們要刪除後面數來第n個node，
如果從前面數來，也就是(鏈結長度 - 1 - n)個node，
要刪除node我們需要知道刪除目標的前一個是誰。  

#### 方法二 : 快慢指標

使用快慢指標來找到正確的節點，做到這一點而不需要先計算LL的總長度。 

* 初始化快慢指標：這段程式碼首先宣告了兩個指標 fast 和 slow，並將它們都初始化為指向的頭節點 head。

* 移動快指標：將 fast 指標向前移動 n 個節點。 這個步驟是為了在 fast 和 slow 之間建立一個長度為 n 的間隔。

* 檢查快指標：如果 fast 指標在這個過程中變成了 null，這表示要刪除的節點實際上是頭節點。 在這種情況下，函數直接傳回 head.next，即刪除了頭節點。

* 同時移動快慢指標：如果不需要刪除頭節點，會進入一個 while 迴圈，這個迴圈會一直持續，直到 fast 指標指向LL的最後一個節點。 在這個迴圈中，fast 和 slow 指標都會同時向前移動，但由於 fast 指標領先 slow 指標 n 個節點，所以當 fast 到達鍊錶末端時，slow 就會剛好位於要刪除節點的前一個節點。

* 刪除節點：在循環結束後，slow.next 是要刪除的節點。 透過將 slow.next 設定為 slow.next.next，我們跳過了要刪除的節點，從而實現了刪除操作。

* 返回鍊錶頭：最後，函數傳回更新後的鍊錶頭 head。

### My Code

#### 方法一
```java
```

#### 方法二 快慢指標
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode fast = head, slow = head;
        for (int i = 0; i < n; i++) fast = fast.next; // fast 先跑n步
        if (fast == null) return head.next;
        while (fast.next != null) {
            fast = fast.next; // fast 指针向前移一步
            slow = slow.next; // slow 指针也向前移一步
        }
        slow.next = slow.next.next;
        return head;
    }
}
```
