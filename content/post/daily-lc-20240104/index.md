---
title: Daily Leetcode - 2870. Minimum Number of Operations to Make Array Empty
description: Medium 與相似題目2244
date: 2024-01-04 12:00:00+0000
categories:
    - LeetCode
    - Greedy
---

##  2024 Jan LC challenge

### 題目  2870. Minimum Number of Operations to Make Array Empty

相似題目 : 2244. Minimum Rounds to Complete All Tasks

### 方法

 
### My Code

#### 方法一

* freq % 3 == 1
直接傳回 -1，因為無法僅透過刪除兩個或三個相同元素的操作來處理只出現一次的元素。

* freq % 3 == 0
這表示可以只透過刪除三個相同元素的操作來處理這個數字。 操作次數是 value / 3。

* freq % 3 == 2 || freq % 3 == 1
這表示除了可以透過刪除三個相同元素的操作處理的部分外，還需要額外一次操作來處理剩餘的一個或兩個元素。 因此，總操作次數是 (value / 3) + 1。

```java
class Solution {
    public int minOperations(int[] nums) {
        Map<Integer, Integer> freq = new HashMap<>();
        for(int num : nums) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }
        int count = 0;
        for (Integer value : freq.values()) {
            if (value == 1) {
                return -1;
            }
            if (value % 3 == 0 ) {
                count += value / 3;
            }else if (value % 3 == 1 || value % 3 == 2){
                count += (value / 3) + 1;
            }else {
                return -1;
            }
        }
        return count;
    }
}
```

### 方法二

freq 表示陣列中某個特定元素的出現次數。 目的是要透過盡可能少的操作次數使數組中的這些元素被完全刪除，每次操作可以刪除兩個或三個具有相同值的元素。 

* freq % 3 == 0：

這表示元素的出現次數是3的倍數。 在這種情況下，可以僅透過刪除三個相同元素的操作來處理這些元素。 操作的次數是 freq / 3，即元素總數除以3。

* freq % 3 == 2：

這意味著元素的出現次數比3的倍數多2。 例如，如果一個元素出現了5次（5 % 3 == 2），你不能只透過刪除三個相同元素的操作來處理所有元素。 首先，你可以刪除 (freq - 2) 個元素（即3個），然後再用一次操作刪除剩下的2個元素。 所以，操作次數是 (freq - 2) / 3 + 1。

* freq % 3 == 1：

這意味著元素的出現次數比3的倍數多1。 需要透過一些操作來處理這些元素。 首先，你刪除 (freq - 4) 個元素（即3的倍數），然後用兩次操作分別刪除剩下的4個元素（一次刪除兩個，另一次刪除兩個）。 所以，操作次數是 (freq - 4) / 3 + 2。


```java

// 其餘略
 if (freq % 3 == 0)
    ans += freq / 3;
else if (freq % 3 == 2)
    ans += (freq - 2) / 3 + 1;
else if (freq % 3 == 1)
    ans += (freq - 4) / 3 + 2;
```



### 2244 題 一個數學向上取整技巧

題目可以用上面那一題去解，雖然題意不太一樣。
這邊主講向上取整 :

```java
class Solution {
    public int minimumRounds(int[] tasks) {
        Map<Integer, Integer> freq = new HashMap<>();
        for (int i : tasks) {
            freq.put(i, freq.getOrDefault( i, 0) + 1);
        }
        int count = 0;
         for(int key: freq.keySet()) {
            int val = freq.get(key);
            if(val==1) return -1;
            count += (val+2)/3;
        }
        return count;
    }
}
```

* 關於這一行 為何要加二
```java
count += (val+2)/3;
```
因為本題是Greedy，計算所需要的最小次數。
那加2是啥意思 ? 加了不會影響結果 ? 

舉例來說 : 

今天 val = 6 :
6 / 3 = 2, 如果 (6 + 2) / 3 = 2 , 其實就沒有變化，效果是一樣的（因為整數除法會捨去小數部分）。

但今天如果是 val = 7 :
7 / 3 = 2 代表我們只操作兩次， 但這至少三次才能吃下他，所以 (7 + 2) / 3 = 3，至少三次。

這種加2的方法在整數除法中是一種有效的技巧，用於確保在計算所需操作次數時能夠向上取整，
反映完成所有任務所需的最小操作次數 。