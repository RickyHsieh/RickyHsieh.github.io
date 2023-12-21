---
title: Daily Leetcode - 237. Delete Node in a Linked List
description: LinkedList 刷爆 奇怪的題目順便補充LL刪除技巧
date: 2023-12-21 12:00:00+0000
categories:
    - LeetCode
    - LinkedList
---

##  2023 Dec LC challenge


### 題目 237. Delete Node in a Linked List

#### 方法

寫一個方法來刪除一個給定的非末尾節點 node，並且規定不能從頭部開始遍歷。

將 node 的下一個節點的值複製到 node，然後讓 node 指向它的下一個節點的下一個節點來實現。 
就是修改 node 的 val 和 next 屬性。

有效地“刪除”給定的非末尾節點。 需要注意的是，這種刪除方法實際上並沒有釋放被「刪除」節點的內存，因為它只是將其從LL的邏輯結構中移除了。 在具有垃圾收集機制的環境（如 Java）中，一旦沒有引用指向原始的下一個節點，它最終會被垃圾收集器回收。

### My Code

#### 方法一

```java
class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

### 刪除節點兩技巧

#### 一、 找到並使用前驅節點進行刪除：(刪除第n個節點)

這種方法涉及遍歷linkedlist直到找到目標節點的前驅節點。
一旦找到前驅節點，您就可以透過改變前驅節點的 next 指標來跳過目標節點，從而實現刪除操作。
這是linkedlist刪除操作中最常見的方法之一，特別是當您需要刪除特定位置的節點時。

#### 二、直接操作 current.next 進行刪除：(刪除多節點或是根據節點的值)

這種方法在遍歷鍊錶時，不是尋找要刪除的節點，而是檢查每個節點的下一個節點（即 current.next）。
如果 current.next 是要刪除的節點，您可以透過將 current.next 設定為 current.next.next 來跳過它。

這種方法在某些情況下更簡潔，尤其是當我需要基於節點的值來刪除節點，而不是基於節點的位置時。
兩種方法都有效，但適用於不同的情境。 第一種方法在您需要根據位置（例如刪除第 n 個節點）來刪除節點時很有用，而第二種方法在您需要根據節點的值來刪除多個節點時更為直接和高效。
