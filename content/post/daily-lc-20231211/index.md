---
title: Daily Leetcode - 67. Add Binary
description: Easy 外加 66. Plus One 十進制二進制進位問題
date: 2023-12-11 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 67. Add Binary

Given two binary strings a and b, return their sum as a binary string.

將兩個Binary 字串做相加，

### My Code

我們從兩字串最尾開始，模擬二進位計算。
* 二進位 1 + 1 = 10 ，寫 0 進位，關於表保留的部分，就是取模餘數 2 % 2 = 0。
* 二進位進位部分，則是 2 / 2 = 1，進 1
* 確保有無需要進位
* 反轉(因為是從最後開始) 

假設有兩個二進制字串 a = "101" 和 b = "110"。

從最右邊的位開始，i = 2，j = 2（字串的最後一位索引）。

第一次，sum = carry + a[2] + b[2] = 0 + 1 + 0 = 1。因此，sb = "1"，carry = sum / 2 = 0。

第二次，sum = carry + a[1] + b[1] = 0 + 0 + 1 = 1。因此，sb = "11"，carry = 0。

第三次，sum = carry + a[0] + b[0] = 0 + 1 + 1 = 2。這時，sb = "011"，carry = 1。

因為所有位都處理完了，但 carry = 1，所以 sb = "1011"。

反轉 sb 得到最終結果 "1101"。

```java
class Solution {
    public String addBinary(String a, String b) {
       
        StringBuilder sb = new StringBuilder();
        int i = a.length() - 1, j = b.length() - 1, carry = 0;
        while (i >= 0 || j >= 0) {
            int sum = carry;
            if (i >= 0) sum += a.charAt(i--) - '0';
            if (j >= 0) sum += b.charAt(j--) - '0';
            //兩位數相加的結果只能是0或1
            //（例如，1 + 1 = 10，在二進制中，我們只寫下0，並將1進位）。
            sb.append(sum % 2);
            carry = sum / 2;
        }
        if (carry != 0) sb.append(carry);
        return sb.reverse().toString();
    }
}
```

carry 在這個上下文中代表進位。在二進制加法中，當兩個數字相加超過1時，就會產生進位。例如，1 + 1 = 0 (在當前位) 並且產生1的進位。carry 變量用於存儲這個進位，並在下一次迭代時將其加到下一對數字的和中。這就是為什麼在計算完當前位的和後，carry 被設置為 sum / 2，這反映了在二進制加法中進位的值。



### 十進制題目

### 66. Plus One

Easy

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.


兩部分處理的是不同情況：

for 循環和他內部的 if 語句處理的是普通情況。如果在數組中找到一個數字小於9，則將該數字加1並立即返回修改後的數組。這是因為加1不會導致進位到更高位。

如果整個數組都遍歷完畢（所有位都是9），則會執行循環外的code：創建一個新的、長度比原數組多1的數組 newArr。這是因為對像 999 這樣的數組加1會導致進位到一個新的最高位（變成 1000）。在這個新數組中，第一位設為1，其餘位（自動初始化為0）保持不變。然後返回這個新數組。

```java
class Solution {
    public int[] plusOne(int[] digits) {
        
        int n = digits.length;
        for(int i = n - 1; i >= 0; i--) {
            if(digits[i] < 9) {
                digits[i]++;
                return digits;
            }
            digits[i] = 0;
        } 
        int[] newArr = new int[n + 1];
        newArr[0] = 1;
        return newArr;
    }
}
```