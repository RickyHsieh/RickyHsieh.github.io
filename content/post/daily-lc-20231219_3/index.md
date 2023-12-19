---
title: Daily Leetcode - 2130. Maximum Twin Sum of a Linked List
description: Medium LinkedList 快慢指標、反轉LL  
date: 2023-12-19 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 2130. Maximum Twin Sum of a Linked List

* 使用快慢指針找到鏈表的中間點。
* 在遍歷過程中，反轉鏈表的前半部分。
* 遍歷鏈表的後半部分，同時與反轉後的前半部分進行成對求和，並記錄下最大的和。
* 返回記錄的最大和。

### My Code


#### 方法
```java
class Solution {
    public int pairSum(ListNode head) {
        // 初始化慢指針和快指針，都指向鏈表的頭部。
        ListNode slow = head;
        ListNode fast = head;

        // 用於反轉鏈表的前半部分。
        ListNode prev = null;
        ListNode temp = null;

        // 使用快慢指針來找到鏈表的中間點，同時反轉鏈表的前半部分。
        while(fast != null && fast.next != null) {
            fast = fast.next.next;

            // 反轉鏈表的過程。
            temp = slow.next;
            slow.next = prev;
            prev = slow;
            slow = temp;
        }

        // 如果鏈表的長度是奇數，則移動慢指針到中間點的下一個節點。(題目已知偶數)
        // if (fast != null) {
        //     slow = slow.next;
        // }

        // 初始化用於記錄最大和的變量。
        int max = 0;

        // 遍歷鏈表的後半部分，並與反轉的前半部分的對應節點進行求和。
        while(slow != null) {
            max = Math.max(max, prev.val + slow.val);
            prev = prev.next;
            slow = slow.next;
        }

        // 返回最大和。
        return max;
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