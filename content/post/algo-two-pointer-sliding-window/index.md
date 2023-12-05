---
title: Algorithm two pointer & sliding window
description:
date: 2023-11-27 00:00:00+0000
categories:
    - Algorithm
---

##  two pointer & sliding window 系列


### Two Pointer

常用於 Array, String, LinkedList

#### 左右指標
概念就是會去設定左右兩個指標，依照情況，移動其中的一個或兩個指標，兩個指標的方向可以是同方向，也可以是反向移動。

#### 快慢指標


### Sliding window

概念就是可以使用一個 pointer 以及一個 window size 去實作，且會利用 window 中的 elements去依照情境去使用，就不用像 two pointer 兩個 pointer 去實作。

### Two Pointer vs Sliding window

差異 :
- two pointer 操作雙指針
- sliding window 主要操作 window 中的 elements 

### LeetCode 練習

#### 3. Longest Substring Without Repeating Characters
Given a string s, find the length of the longest substring without repeating characters.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int longest = 0;
        Map<Character, Integer> map = new HashMap<>();

        for (int i = 0, j = 0; j < s.length(); j++) {
            
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            
            longest = Math.max(longest, j - i + 1);

            map.put(s.charAt(j), j + 1);

        }

        return longest;


    }
}
```

### 26. Remove Duplicates from Sorted Array


```java
class Solution {
    public int removeDuplicates(int[] nums) {

        if (nums.length == 0) return 0;
        
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```

### 80. Remove Duplicates from Sorted Array II

解題想法:
* 已排序(小到大)
* case 1: 沒有重複
* case 2: 有重複且必須 < 2，只要小於2 處理方式幾乎就跟 case 1 一樣了 !
* 指針 i 是為要插入的位置
* 指針 j 是單純遍歷

```java
class Solution {
    public int removeDuplicates(int[] nums) {

        if (nums.length == 0) return 0;

        int i = 0;
        int count = 1;
        for (int j = 1; j < nums.length; j++) {
            
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
                count = 1;
            } else {
                
                if ( count < 2) {
                    i++;
                    nums[i] = nums[j];
                    count++;
                }
            }
        }
        return i + 1;
    }
}
```

大神的作法:

解析:

* 已排序
* i 為要插入值的位置
* 使用 for-each 去遍歷陣列
* i < 2 表示，如果要有重複值出現至少要大於2，題目限制重複2次可以，所以無論如何最初前兩個一定會被加到陣列中，簡而言之，前兩個一定會在我們最後答案的陣列中。
* n > nums[i-2] 代表針對排除陣列最前面兩項後，來做排序，而因為由小到大，所以如果
n > nums[i-2] 代表，大於前面的數字，也代表沒出現過。

```java
public int removeDuplicates(int[] nums) {
    int i = 0;
    for (int n : nums)
        if (i < 2 || n > nums[i-2])
            nums[i++] = n;
    return i;
}
```
Note:
```java
nums[i++] = n;
```
等同
```java
nums[i] = n;
i++;
```

### 977. Squares of a Sorted Array

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

給一個數組，平方，其中會有負數。

解法一: 暴力法，先平方在比大小
解法二: two pointer，先絕對值比大小在平方和塞到新數組

#### 解法一

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        
       for (int i = 0; i < nums.length; i++) {
            int positive = Math.abs(nums[i]);
            nums[i] = (int) Math.pow(positive, 2);
        }
        Arrays.sort(nums);
        return nums;
    }
}
```
* 平方操作：遍歷整個數組並對每個元素進行平方，其時間複雜度為O(n)，
 其中 n 是數組 nums 的長度。

* 排序操作：使用 Arrays.sort() 對數組進行排序，其平均時間複雜度為O(nlogn)。
 綜合來看，解法一的總時間複雜度O(nlogn)，因為排序操作占主導。

* 空間複雜度
 這種方法直接在輸入數組 nums 上操作，並沒有使用額外的顯著空間（除了幾個基本變量外）。因此，其空間複雜度為O(1)。

#### 解法二
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        
       int n = nums.length;
       int[] result = new int[n];
       int left = 0, right = n - 1;

        for (int i = n - 1; i >= 0; i--) {

            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                result[i] = (int)Math.pow(nums[left],2);
                left++;
            } else {
                result[i] = (int)Math.pow(nums[right],2);
                right--;
            }

        }
        return result;

    }
}
```
* 時間複雜度

雙指針操作：通過一次遍歷來填充結果數組 result。每個元素僅被訪問一次，因此時間複雜度為O(n)。
這種方法利用了原始數組的已排序特性，避免了額外的排序操作，因此總時間複雜度為O(n)。

* 空間複雜度
這種方法使用了一個額外的數組 result 來存儲結果，這個數組與輸入數組 nums 大小相同。因此，其空間複雜度為 O(n)。

* 結論
解法一的時間複雜度為 O(nlogn)，空間複雜度為O(1)。
解法二的時間複雜度為 O(n)，空間複雜度為O(n)。
因此，如果空間不是一個主要考慮因素，解法二在效率上更佳，尤其是在數組較大時。

