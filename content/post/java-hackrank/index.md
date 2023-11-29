---
title: HackerRank - Java Static Initializer Block
description:
date: 2022-03-06 00:00:00+0000
image:
categories:
    - HackerRank
tags:
    - HackerRank
---


## what is static initialize ?

Static Initialization Blocks

作用：用於初始化類別變數（靜態變數），尤其是當初始化需要某一些邏輯（例如錯誤處理或迴圈）時。
定義：由靜態關鍵字 static 和花括號 {} 包圍的程式碼區塊。
可以有多個靜態初始化區塊，它們按照在類別中出現的順序執行。
例如：

```java
static {
     // 初始化程式碼
}
```
private static initialze：作為靜態初始化區塊的替代方案，可以用於稍後重新初始化類別變數。

## Here is my code 


```java
import java.io.*;
import java.util.*;

public class Solution {
    
    static int breadth;
    static int height;
    static boolean flag;
    
    static {
        Scanner sc = new Scanner(System.in);
        breadth = sc.nextInt();
        height = sc.nextInt();
        if (breadth > 0 && height > 0) {
            flag = true;
        } else {
            System.out.println("java.lang.Exception: Breadth and height must be positive");
        }
    }

    public static void main(String[] args) {

        if (flag) {
            long area = height * breadth;
            System.out.println(area);
        }
    
    }
}
```

