---
title: Daily Leetcode - 82. Remove Duplicates from Sorted List II
description: Medium linkedList 刷爆周 刪除 node (所有有重複的)
date: 2023-12-22 13:00:00+0000
categories:
    - LeetCode
    - Array
---

##  2023 Dec LC challenge

### 題目 82. Remove Duplicates from Sorted List II

即在排序鏈結中刪除所有重複的節點。
```
1 - 2 - 3 - 3 - 4 ->
to
1 - 2 - 4 - >
```

首先會想到如何跳過重複的節點: 
* 我需要追蹤重複點的前一個node
* 以及使用啞節點（dummy node）來處理頭部可能是重複節點的情況。這是處理此類問題的常見方法。
* 使用while迴圈跳過重複點，while迴圈會停在最後的重複點，所以要將該重複點再往下一個點，再給dummy.next 引用。

### My Code

#### 方法一

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
    public ListNode deleteDuplicates(ListNode head) {
        
        if(head == null) return head;
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode current = head;

        while(current != null) {

            if(current.next != null && current.val == current.next.val) {
                while(current.next !=null && current.val == current.next.val) {
                    current = current.next;
                }
                prev.next = current.next;
            } else {
                prev = current;
            }
            current = current.next;
        }
        return dummy.next;
    }
}
```