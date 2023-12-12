---
title: Daily Leetcode - 2390. Removing Stars From a String
description: Medium 使用Stack 和 Sliding window
date: 2023-12-12 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 2390. Removing Stars From a String

You are given a string s, which contains stars *.

In one operation, you can:

Choose a star in s.
Remove the closest non-star character to its left, as well as remove the star itself.
Return the string after all stars have been removed.


### My Code

### 解法一

```java
class Solution {
    public String removeStars(String s) {
       StringBuilder sb = new StringBuilder();

       for (int i = 0; i < s.length(); i++) {
           if (s.charAt(i) == '*') {
            sb.deleteCharAt(sb.length() - 1);
           } else {
            sb.append(s.charAt(i));
           }
       } 
       return sb.toString();
    }
}
```

#### 時間複雜度：
遍歷字串 s 一次，時間複雜度為 O(n)，其中 n 是字串 s 的長度。
對於 StringBuilder 的每次 deleteCharAt 和 append 操作，平均時間複雜度通常視為 O(1)，因為 StringBuilder 在內部維護一個足夠大的字元數組，因此添加和刪除操作通常不需要重新分配記憶體。
因此，第一個解決方案的總體時間複雜度是 O(n)。

#### 空間複雜度：
使用了一個 StringBuilder 來儲存中間結果，其大小最多與輸入字串 s 的長度相等，因此空間複雜度為 O(n)。


### 解法二

#### 時間複雜度：
遍歷字串 s 一次，時間複雜度為 O(n)。
對於堆疊的每次 push 和 pop 操作，時間複雜度是 O(1)。
在建構最終字串時，透過 sb.insert(0, stack.pop()) 遍歷堆疊一次，時間複雜度為 O(n)。
因此，第二個解決方案的整體時間複雜度也是 O(n)。

#### 空間複雜度：
使用了一個堆疊來儲存字符，其大小最多與輸入字串 s 的長度相等，空間複雜度為 O(n)。
```java
class Solution {
    public String removeStars(String s) {
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            if(s.charAt(i) != '*') {
                stack.push(s.charAt(i));
            }else if (!stack.isEmpty()) {
                stack.pop();
            }
        }
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.insert(0, stack.pop());
        }
        return sb.toString();
    }
}
```