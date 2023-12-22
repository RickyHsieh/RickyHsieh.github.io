---
title: Daily Leetcode - 61. Rotate List
description: LinkedList 刷爆 旋轉LinkedList
date: 2023-12-22 12:00:00+0000
categories:
    - LeetCode
    - LinkedList
---

##  2023 Dec LC challenge


### 題目 61. Rotate List

#### 方法

* 遍歷鍊錶以確定長度：確定鍊錶的長度 n（在這個例子中為 5）。

* 確定旋轉點：計算旋轉 k 次後鍊錶的新尾部位置。 在這個例子中，旋轉 2 次，新尾部是第 5 - 2 = 3 個節點（即節點 3）。

* 執行旋轉：斷開新尾部和後面節點的連接，並將後面的部分移到鍊錶的前面。 同時，將原來的尾部節點的 next 指向原來的頭部節點。

#### 做法

* 計算鏈結長度：
  遍歷鏈結以確定其長度。
* 形成環：
  將鏈結的尾部連接到頭部，形成一個環。
* 找到新尾部：
  根據旋轉次數 k 和鏈結長度 length，找到新的尾部節點（newTail）。
* 斷開環：
  在新的尾部節點斷開環，並設定新的頭部節點。

#### 關於鏈結旋轉

* length - k % length - 1 是在鏈結旋轉操作中用來決定新的尾部節點位置的:

  length：這是鏈結的總長度。
  k % length：這裡 k 是想要右旋轉鏈結的次數。
  % 是模運算，k % length 計算了實際的旋轉次數，這是為了處理 k 大於鏈結長度的情況。 例如，如果鍊錶長度是 5，而 k 是 7，那麼旋轉 7 次和旋轉 2 次（因為 7 % 5 = 2）的效果是相同的。

* length - k % length：
  這一部分計算了在鍊錶中從頭節點開始到新尾部節點的距離。 為什麼要用 length - k % length 呢？ 因為右旋轉 k 次相當於將鍊錶尾部的 k % length 個節點移動到了鍊錶的開頭。

* length - k % length - 1：

  最後，減去 1 是為了找出新尾部節點的前一個節點。 這是因為在確定新尾部之後，我們需要在該節點處斷開鍊錶，以形成新的頭部和尾部。 如果我們直接定位到新尾部，我們就沒有辦法方便地斷開鍊錶。

### My Code

#### 方法

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        // 單一node、空鏈結無法rotate
        if(head == null || head.next == null || k == 0) return head;
        
        // 計算鏈結長度
        ListNode oldTail = head;
        int length = 1;
        while(oldTail.next != null) {
            length++;
            oldTail = oldTail.next;
        }

        // 形成環
        oldTail.next = head;

        ListNode newTail = head;
        for(int i = 0; i < length - k % length - 1 ; i++) {
            newTail = newTail.next;
        }
        // 遍歷結束，此時newTail是新尾部節點的前一個
        ListNode newHead = newTail.next;
        // 斷開環
        newTail.next = null;

        return newHead;

    }
}
```