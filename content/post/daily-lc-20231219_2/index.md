---
title: Daily Leetcode - 2095. Delete the Middle Node of a Linked List
description: Medium Linkedlist 快慢指標  
date: 2023-12-19 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 2095. Delete the Middle Node of a Linked List

使用快慢指標找到中間點在做刪除。

* 快慢指標找中間點
* 刪除處理

### My Code

* fast 走兩步
* slow 走一步
* 要刪除鏈結需要知道，刪除目標的前一個節點。

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
    public ListNode deleteMiddle(ListNode head) {
        
        if (head == null) return null;

        ListNode fast = head;
        ListNode slow = head;
        ListNode prev = null; // 刪除節點要知道前一個節點

        while(fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        // slow 指向中間節點，pre 指向slow前一節點
        if (prev != null) {
            prev.next = slow.next;
        } else {
            //是最開頭的點
            head = head.next;
        }
        return head;
    }
}
```

#### 刪除節點虛擬碼

```java
function deleteNode(head, target):
    if head is null:
        return head  // 空鏈結，不須刪除
    
    if head.value == target:
        // 删除頭節點
        head = head.next
        return head

    current = head
    while current.next is not null:
        if current.next.value == target:
            current.next = current.next.next  // 删除下一個節點
            return head
        current = current.next

    return head  // 如果未找到目標節點則不變

```

#### 新增節點虛擬碼

```java
function insertNode(head, newNode, position):
    if position == 0:
        // 在鏈結插入節點
        newNode.next = head
        head = newNode
        return head

    current = head
    count = 0
    while current is not null:
        count++
        if count == position:
            // 在當前節點後插入節點
            newNode.next = current.next
            current.next = newNode
            return head
        current = current.next

    // 如果 position 超出鏈結長度，可以選擇插入到尾部
    // 或者根據需要執行其他操作
    return head
```