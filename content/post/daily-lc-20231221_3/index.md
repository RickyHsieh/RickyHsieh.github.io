---
title: Daily Leetcode - 876. Middle of the Linked List
description: LinkedList 刷爆 快慢指標找中間值技巧
date: 2023-12-21 12:00:00+0000
categories:
    - LeetCode
    - LinkedList
---

##  2023 Dec LC challenge


### 題目 876. Middle of the Linked List

#### 方法

看到找中間值 =====> 考慮快慢指標(注意基數或是偶數問題)

假設我們有一個singly LL，其節點數為奇數，例如：
```
1 -> 2 -> 3 -> null
```

原本我寫的迴圈的條件是
``` 
while(fast.next != null)
```
這表示迴圈會繼續，只要 fast.next 不是 null。 讓我們一步一步地看看會發生什麼：

* 初始時，fast 和 slow 都指向頭節點（值為 1）。

* 第一次循環迭代後：

fast 將移動兩步，指向 null（因為從節點 3 移動兩步就到了LL的末端）。
slow 將移動一步，指向節點 2。
現在，因為 fast 是 null，所以在嘗試檢查 fast.next 時，程式碼將引發空指標異常。

為了避免這個問題，正確的迴圈條件應該是 while(fast != null && fast.next != null)。 這樣，在鍊錶長度為奇數時（如上例），當 fast 到達最後一個節點（3）時，它的 next 是 null，迴圈將在再次嘗試移動 fast 之前終止。 這就意味著 slow 將停在中間節點（在這個例子中是 2）。

所以，修正後的程式碼能夠正確處理奇數長度的鍊錶，同時也適用於偶數長度的鍊錶。 
在偶數長度的鍊錶中，slow 將指向兩個中間節點中的第二個。


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
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next; 
        }
        return slow;
    }
}
```

