---
title: LinkedList 實作
description: 使用Java實作LL
date: 2023-12-27 12:00:00+0000
categories:
    - Data Structure
---

##  LinkedList in Java

### Code

```java
public class ListNode {
    
    int val; // 節點值

    ListNode next; // 指向下一個

    public ListNode() { // 節點 contructor
    }

    public ListNode(int val) { // 節點 contructor
        this.val = val;
    }

    public ListNode(int val, ListNode next) { // 節點 contructor
        this.val = val;
        this.next = next;
    }
}
```

#### 說明

* 成員變數：

    int val;：這是結點儲存的數據，通常是整數型別。
    ListNode next;：這是指向鍊錶中下一個結點的參考。

* 無參構造函數 public ListNode()：

    這個建構函式建立一個沒有資料和下一個節點引用的空結點。

* 帶有一個參數的建構子 public ListNode(int val)：

    這個建構函式建立一個包含特定值 val 的結點，但沒有指定下一個節點，即 next 預設為 null。

* 有兩個參數的建構子 public ListNode(int val, ListNode next)：

    這個建構函式建立一個包含特定值 val 的結點，並指定其下一個節點為 next。
    這個 ListNode 類別是建立單鍊錶的基礎。 使用它來建立LL，例如：

```java
public class LinkedListDemo {
    public static void main(String[] args) {
        ListNode node1 = new ListNode(1);
        ListNode node2 = new ListNode(2);
        ListNode node3 = new ListNode(3);

        node1.next = node2;
        node2.next = node3;

        ListNode current = node1;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }
}

```