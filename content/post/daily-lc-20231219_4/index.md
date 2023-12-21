---
title: Daily Leetcode - 206. Reverse Linked List
description: 反轉LL技巧 常用技巧!!!!  
date: 2023-12-19 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 206. Reverse Linked List

* 通常會使用到三個指標
three pointers here: prev, cur and next.

### My Code

#### 方法
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode current = head;
    ListNode next = null;

    while (current != null) {
        next = current.next; // 保存當前節點的下一個節點
        current.next = prev; // 改變當前節點的指針指向前一個節點
        prev = current; // 將 prev 和 current 向前移動
        current = next;
    }

    head = prev; // 更新頭節點
    return head;
}
```

```c
def reverseListRecursive(self, head):
    def reverse(cur, prev):
        if cur is None:
            return prev
        else:
            next = cur.next
            cur.next = prev
            return reverse(next, cur)

    return reverse(head, None)

```

#### 遞迴方式

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
        next = null;
    }
}

public class Solution {
    public ListNode reverseLinkedList(ListNode head) {
        // 遞歸的基本情況：如果頭節點是 null 或者是最後一個節點，則不需要進一步的反轉
        if (head == null || head.next == null) {
            return head;
        }

        // 遞歸反轉鏈表的剩餘部分
        ListNode reversedListHead = reverseLinkedList(head.next);

        // 將當前節點的下一個節點指向當前節點，從而實現反轉
        head.next.next = head;

        // 斷開當前節點的下一個指針，以避免循環
        head.next = null;

        // 返回反轉後的鏈表頭節點
        return reversedListHead;
    }
}

```