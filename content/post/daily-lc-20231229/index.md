---
title: Daily Leetcode - 141. Linked List Cycle
description: Easy LinkedList 環形
date: 2023-12-27 12:00:00+0000
categories:
    - LeetCode
    - LinkedList
---

##  2023 Dec LC challenge

### 題目  141. Linked List Cycle

* 確認有環
* 找入口

#### 確認有環
使用快慢指標，一個快指標、一個慢指標，就想像成跑步相對速度一個跑得快，一個跑得慢，總會相遇。

#### 找到入口

[帶把隨想錄](https://www.programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E6%80%9D%E8%B7%AF)

### My Code

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow) {
                ListNode index1 = fast;
                ListNode index2 = head;
                while(index1 != index2) {
                    index1 = index1.next;
                    index2 = index2.next;
                }
                return index1;
            }
        }
        return null;
    }
}
```

#### 說明
