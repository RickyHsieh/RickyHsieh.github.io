---
title: Angular crash Introduction
description: An
date: 2023-12-22 13:00:00+0000
categories:
    - LeetCode
    - Array
---

##  Angular 簡介

Angular is a framework for building modern single-page applications.

## 關於 TypeScript 

TypeScript 是一種由微軟開發的開源程式語言。 
它是JavaScript的一個超集，增加了可選的靜態類型和基於類別的物件導向程式設計。

#####  以下是TypeScript的一些主要特點：

* 靜態型別檢查：
    與JavaScript不同的是，TypeScript在程式碼編寫階段就能檢查型別錯誤。 這意味著開發者可以在程式碼運行之前發現並修正錯誤，這有助於提高程式碼品質和可維護性。

* 類型推斷：
    TypeScript能夠自動推斷變數的類型，減少了顯示類型宣告的需要。

* 支援最新的JavaScript特性：
    TypeScript支援ECMAScript標準的最新特性，例如箭頭函數、非同步/等待等，並將它們編譯成舊版本的JavaScript，以確保相容性。

* 豐富的IDE支援：
    由於具有類型訊息，TypeScript在整合開發環境（IDE）中能提供更好的自動完成、導航和重構功能。

* 類別、介面和模組：
    TypeScript支援基於類別的物件導向編程，包括類別、介面和模組等概念，這使得建立大型應用程式更為方便。

* 跨瀏覽器、跨裝置、跨平台：TypeScript最終被編譯為JavaScript，因此可以在任何支援JavaScript的瀏覽器、裝置或平台上執行。

* 社群支持與生態系統：TypeScript由於微軟的支持和廣泛的社群參與，具有豐富的生態系統，包括大量的函式庫和工具。

TypeScript特別適合用於開發大型或複雜的JavaScript應用程序，它提供了強大的工具和實踐來管理大型程式碼庫和團隊。

## compile the code 

web browsers do not understand Typescript natively, have to convert to JS code.

This is known as "transpiling".

trsnspiling : translating / compiling.

"Transpiling"（或稱為"原始碼到原始碼編譯"）是一個程式設計術語，指的是將一種程式語言的原始程式碼轉換為另一種語言的等效程式碼。 這個過程不同於傳統的編譯，因為它通常涉及兩種高階語言之間的轉換，而不是將高階語言轉換為低階語言（如組合語言或機器碼）。

在TypeScript的上下文中，transpiling是一個非常重要的概念。 TypeScript是JavaScript的一個超集，這意味著任何有效的JavaScript程式碼也是有效的TypeScript程式碼。 但是，TypeScript增加了一些不屬於JavaScript的特性，例如靜態類型檢查和更豐富的物件導向程式設計模型。 這些特性在執行時期的JavaScript環境中並不存在。


mydemo.ts ==== tsc ====> mydemo.js

```
```