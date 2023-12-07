---
title: Daily Leetcode - 60. Permutation Sequence
description: 2023 Dec LC challenge Day 7 
date: 2023-12-07 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

#### 60. Permutation Sequence




## My Code

您的 Solution 類別中的 getPermutation 方法目標是取得給定數 n 的所有排列中的第 k 個排列。 這個方法先產生所有排列，然後選擇第 k 個。 然而，這種方法在 n 較大時可能會導致逾時，因為它需要產生 n!（n 的階乘）個排列，這在 n 增大時非常耗時且耗記憶體。

要最佳化這個問題，您可以使用一種不需要產生所有排列的方法來直接計算第 k 個排列。 這種方法是基於觀察到排列的特定模式，可以透過計算而非完全枚舉來得到結果。 以下是一個改進的實作：

```java

class Solution {
    public String getPermutation(int n, int k) {
        
        int[] array = new int[n];
        for (int i = 0; i < n; i++) {
            array[i] = i + 1;
        }
        List<Integer> permuted = permute(array).get(k-1);
        
        String ans = "";
        for(int i = 0; i < permuted.size(); i++) {
          ans += String.valueOf(permuted.get(i));
        }

        return ans;
    }

    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> resultList = new ArrayList<>();
        backtracking (resultList, new ArrayList<>(), nums);
        return resultList;
    }

    public void backtracking (List<List<Integer>> resultList, ArrayList tempList, int[] nums) {

        if (tempList.size() == nums.length) {
            resultList.add(new ArrayList<>(tempList));
            return;
        }

        for (int num : nums) {     
            if (tempList.contains(num)) {
                continue;
            }
            tempList.add(num);
            backtracking(resultList, tempList, nums);
            tempList.remove(tempList.size() - 1);
        }
    }

    
}
```

#### 字元型數字轉換為對應的整數數字
