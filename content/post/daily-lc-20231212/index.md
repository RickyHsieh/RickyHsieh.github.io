---
title: Daily Leetcode - 1657. Determine if Two Strings Are Close
description: Easy 外加 66. Plus One 十進制二進制進位問題
date: 2023-12-12 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 1657. Determine if Two Strings Are Close

題目要求判斷兩個字串是否可以透過以下兩種操作變得相似：

操作1：交換任意兩個現有字符。
例如，將"abcde"轉換成"aecdb"。

操作2：將現有字符中的一個字符轉換為另一個現有字符，然後對另一個字符執行相同操作。
例如，將"aacabb"轉換成"bbcbaa"（所有的'a'變成'b'，所有的'b'變成'a'）。

你可以使用這兩種操作來改變字串，而且可以根據需要多次應用操作。

給定兩個字串word1和word2，如果可以通過這些操作使它們相似，則返回true；否則返回false。

### My Code

```java
class Solution {
    public boolean closeStrings(String word1, String word2) {
        if (word1.length() != word2.length()) {
            return false;
        }

        int[] count1 = new int[26];
        int[] count2 = new int[26];

        for (char c : word1.toCharArray()) {
            count1[c - 'a']++;
        }

        for (char c : word2.toCharArray()) {
            count2[c - 'a']++;
        }

        for (int i = 0; i < 26; i++) {
            if ((count1[i] == 0 && count2[i] != 0) || (count1[i] != 0 && count2[i] == 0)) {
                return false;
            }
        }

        Arrays.sort(count1);
        Arrays.sort(count2);

        return Arrays.equals(count1,count2);
    }
}
```

```java
class Solution {
    public boolean closeStrings(String word1, String word2) {
        
        // 檢查兩個字串的長度是否相同，如果不相同則不可能是相似的
        if (word1.length() != word2.length()) {
            return false;
        }
        // 創建兩個array，用於記錄字符的出現次數
        int[] count1 = new int[26];
        int[] count2 = new int[26];

        // Count character frequencies in word1
        for (char c : word1.toCharArray()) {
            count1[c - 'a']++;
        }

        // Count character frequencies in word2
        for (char c : word2.toCharArray()) {
            count2[c - 'a']++;
        }

        // Check if the character sets (non-zero counts) are the same in both strings
        for (int i = 0; i < 26; i++) {
            if ((count1[i] == 0 && count2[i] != 0) || (count1[i] != 0 && count2[i] == 0)) {
                return false;
            }
        }

        // Sort the frequency arrays and check if they are the same
        Arrays.sort(count1);
        Arrays.sort(count2);

        for (int i = 0; i < 26; i++) {
            if (count1[i] != count2[i]) {
                return false;
            }
        }

        return true;
    }
}

```