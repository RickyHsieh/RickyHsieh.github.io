---
title: Daily Leetcode - 21. Merge Two Sorted Lists
description: LinkedList 刷爆 結合兩個已排序LinkedList
date: 2023-12-21 12:00:00+0000
categories:
    - LeetCode
    - LinkedList
---

##  2023 Dec LC challenge


### 題目 21. Merge Two Sorted Lists

#### 方法

### My Code

#### 方法一 iteration

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
      ListNode dummy = new ListNode(-1);
      ListNode current = dummy;
      while(l1 != null && l2 != null) {
        if(l1.val < l2.val) {
            current.next = l1;
            l1 = l1.next;
        }else{
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next;
      }

      if(l1 != null) {
        current.next = l1;
      } else if(l2 != null) {
        current.next = l2;
      }

      return dummy.next;

    }
}
```

#### 方法二 recursion

```java

```