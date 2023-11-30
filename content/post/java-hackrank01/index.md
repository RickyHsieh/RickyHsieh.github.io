---
title: HackerRank - Java Lexicographical Comparison
description:
slug:
date: 2023-11-28 00:00:00+0000
image: hk-cover2.jpg
categories:
    - HackerRank
tags:
    - HackerRank
---

## what is Lexicographical Comparison ?

"字典序比較"（Lexicographical Comparison）是電腦科學中用來比較兩個字串的一種方法。 它的基本原理是按照字符的順序逐個比較字串中的字符，就像在字典中查找單字一樣。 

這種比較方式在多種程式設計場景中非常有用，包括字串排序、資料庫查詢最佳化和文字處理等。

## 基本原理

* 字元比較：字典序比較從兩個字串的第一個字元開始，逐一比較對應位置的字元。
* Unicode/ASCII 值：比較基於字元的Unicode或ASCII值。 Unicode是一個國際標準，定義了文字字元的數字編碼，而ASCII是Unicode的一個子集，只包含英文字元和控製字元。
* 終止條件：這種比較會持續到找到不同的字符，或者某個字串先到達末尾。

## 應用場景
字串排序：在陣列或清單排序時，經常使用字典序作為標準。
資料庫查詢：資料庫中的字串欄位經常根據字典序進行索引和查詢。
文字搜尋：在文字搜尋中，字典序可以用來快速定位和比較字串。

## Here is my code

```java
import java.util.Scanner;
public class Solution {

    public static void main(String[] args) {
        
        Scanner sc = new Scanner(System.in);
        String A = sc.next();
        String B = sc.next();

        // Sum the lengths of A and B
        System.out.println(A.length() + B.length());

        // Determine if A is lexicographically larger than B
        System.out.println(A.compareTo(B) > 0 ? "Yes" : "No");

        // Capitalize the first letter of A and B and print them
        System.out.println(capitalizeFirstLetter(A) + " " + capitalizeFirstLetter(B));
    }

    public static String capitalizeFirstLetter(String input) {
        if (input == null || input.isEmpty()) {
            return input;
        }
        return input.substring(0, 1).toUpperCase() + input.substring(1);
    }
}
```