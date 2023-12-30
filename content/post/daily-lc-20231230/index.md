---
title: Daily Leetcode - 202. Happy Number
description: Easy 快慢指標和HashSet解
date: 2023-12-27 12:00:00+0000
categories:
    - LeetCode
    - LinkedList
---

##  2023 Dec LC challenge

### 題目  202. Happy Number


### My Code

trick:
不快樂數 : 4 -> 16 -> 37 -> 258 > 85 -> 145 -> 42 -> 20 -> 4 會進入一個循環。

#### 快慢指標解

快慢指標如果有解最終會指向 1。

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n;
        int fast = getNext(n);
        do {
            slow = getNext(slow);
            fast = getNext(getNext(fast));
        } while(fast != 1 && fast != slow);
        return fast == 1;
    }

    private int getNext(int number) {
        int totalSum = 0;
        while (number > 0) {
            int d = number % 10;
            number = number / 10;
            totalSum += d * d;
        }
        return totalSum;
    }
}
```

* 慢指標（Slow Pointer）：這個指標每次移動一步。 在這個上下文中，"一步" 意味著對當前數字執行平方和的運算。 例如，如果慢指標目前指向數字 19，那麼它下一步會指向82。

* 快指標（Fast Pointer）：這個指標每次移動兩步驟。 他執行兩次平方和的運算。 繼續上面的例子，如果快指標目前指向 19，那麼它的下一步是先移動到 82，然後再根據 82 的平方和進行下一步移動。 所以，如果 82 的平方和是68，那麼快指針將會移動到 68。

* 偵測循環或到達 1：如果數字是快樂數，這個過程最終會讓數字變成 1。 這意味著快指針或慢指針（或兩者）會最終到達 1。 如果數字不是快樂數，那麼快指標和慢指標最終會在某個數字上相遇，這意味著它們進入了一個循環，而這個循環中不包含 1。

* 終止條件：這個方法的終止條件是快指針到達 1（意味著找到了一個快樂數），或者快慢指針相遇（意味著不是快樂數，因為它們陷入了循環）。

這種快慢指針是一種有效的檢測循環存在的方法。

#### HashSet 解


```java
class Solution {
    public boolean isHappy(int n) {

        Set<Integer> nums = new HashSet<>();

        while (n != 1) {
            int temp = 0;
            while(n != 0) {
              int digit = n % 10; //位數
              temp += digit * digit;
              n = n / 10;
            }
            if(!nums.add(temp)) {
                return false;
            }
            n = temp;
        }
        return true;
    }
}
```