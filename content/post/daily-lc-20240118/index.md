---
title: Daily Leetcode - 459. Repeated Substring Pattern
description: Easy
date: 2024-01-18 12:00:00+0000
categories:
    - Math
---

##  2024 Jan LC challenge

### 題目  459. Repeated Substring Pattern

### 方法

序列 abcabc 很明顯，是由可以由abc組成，兩個abc前半後半都相同，
所以將abcabc + abcabc ，勢必會在中間再找到一個 abcabc。
但這兩個相加的字串，需要去頭去尾，否則沒有意義(如果開頭沒擋或結尾沒有擋，無法匹配到中間的)。

### My code 

### 方法一

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        String s2 = s + s;
        s2 = s2.substring(1, s2.length() - 1);
        return s2.contains(s);
    }
}
```

### 方法二 KMP解法

