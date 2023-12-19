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

```c++
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