---
title: Daily Leetcode - 28. Find the Index of the First Occurrence in a String
description: Easy 想法有點打結
date: 2023-12-11 16:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 67. Add Binary

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

 
### My Code


兩個方法意思都差不多，需要注意的是每次比對到不同時，我只把needle從頭算起，但haystack依然接續下去，這樣可能會錯過，所以，haystack 也需要回溯到最初匹配開始的下一个字符，以確保不會錯過任何潛在的匹配。

#### 方法一
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int haystackLen = haystack.length();
        int needleLen = needle.length();

        if (needleLen == 0) {
            return 0;
        }

        for (int i = 0; i <= haystackLen - needleLen; i++) {
            int j;
            for (j = 0; j < needleLen; j++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    break;
                }
            }
            if (j == needleLen) {
                return i;
            }
        }
        return -1;
    }
}
```


#### 方法二

```java
class Solution {
    public int strStr(String haystack, String needle) {
        
        int haystacklen = haystack.length();
        int needlelen = needle.length();
        int needleIndex = 0;
        for (int i = 0; i < haystacklen; i++) {

            if (haystack.charAt(i) == needle.charAt(needleIndex)) {
                needleIndex++;
            } else {
                i = i - needleIndex;
                needleIndex = 0;
            }

            if (needleIndex == needlelen) {
                return i - needlelen + 1;
            }

        }
        return -1;
    }
}
```