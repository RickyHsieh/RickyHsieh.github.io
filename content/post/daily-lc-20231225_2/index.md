---
title: Daily Leetcode - 2089. Find Target Indices After Sorting Array
description: Easy 二分法 計數器活用
date: 2023-12-25 12:00:00+0000
categories:
    - LeetCode
    - 二分法
---

##  2023 Dec LC challenge

### 題目 2089. Find Target Indices After Sorting Array

用兩次二分法找target最初位置到最後一個位置的所有滿足target的索引。


### My Code

#### 方法一 二分法
```java
class Solution {
    public List<Integer> targetIndices(int[] nums, int target) {
        Arrays.sort(nums);
        List<Integer> ans = new ArrayList<>();
        int start = findPosition(nums, target, true);
        if (start == nums.length || nums[start] != target) return ans;
        int end = findPosition(nums, target, false) - 1;
        for (int i = start; i <= end; i++) {
            ans.add(i);
        }
        return ans;
    }

    public int findPosition(int[] nums, int target, boolean findStart) {
        int left = 0;
        int right = nums.length;
        while(left < right) {
            int mid = left + (right - left)/2; 
            if(nums[mid] > target || findStart && nums[mid] == target) {
                right = mid;
            } else{
                left = mid + 1;
            }
        }
        return left;
    }
}
```

#### 方法二 計數器活用

利用兩個計數器
* 一個計算出現target的次數
* 一個計算小於target的次數

```java
class Solution {
    public List<Integer> targetIndices(int[] nums, int target) {
        int equalCount = 0;
        int lessCount = 0;
        for(int num : nums) {
            if(num == target) equalCount++;
            if(num < target) lessCount++;
        }
        List<Integer> result = new ArrayList<>();
        for(int i = 0; i < equalCount; i++) {
            result.add(lessCount+i);
        
        }
        return result;
    }
}
```

假設我們有陣列 nums = [1, 2, 4, 3, 2, 4, 4] 和目標值 target = 4。

計算 lessCount 和 equalCount：

遍歷數組 nums，我們發現 1, 2, 2, 3 這四個元素小於 4（target），所以 lessCount = 4。
同時，有三個元素等於 4（target），所以 equalCount = 3。
建立結果列表：

由於有 4 個元素小於 4，這意味著第一個等於 4 的元素的索引是 4（因為陣列索引從 0 開始）。 所以，lessCount 就是等於 target 的第一個元素的索引。
我們需要將 equalCount（即 3）個索引新增到結果清單中，這些索引分別是 4, 5, 6（這是因為在我們的範例陣列中，4 這個值連續出現了三次）。
因此，for 迴圈中的 result.add(lessCount + i); 將會計算並加入這些索引：

第一次迴圈時，i = 0，所以新增的索引是 lessCount + 0 = 4。
第二次迴圈時，i = 1，所以加入的索引是 lessCount + 1 = 5。
第三次循環時，i = 2，所以新增的索引是 lessCount + 2 = 6。
最終，result 列表將包含 [4, 5, 6]，這就是數組 nums 中所有等於 4 的元素的索引。