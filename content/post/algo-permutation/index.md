---
title: Algorithm permutation & backtracking
description: 全排列以及回溯演算法(待完成)
date: 2023-11-27 00:00:00+0000
categories:
    - Algorithm
---

##  Permutation 



## Backtracking



## My Code

LeetCode

#### 46. Permutations

* 使用 遞迴
* 使用 trackBacking (因為要找出所有可能，使用回溯法)
* 元素皆出現一次

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        
        List<List<Integer>> resultList = new ArrayList<>();
        backtracking(resultList, new ArrayList<>(), nums);
        return resultList;
    }

    private void backtracking(List<List<Integer>> resultList, ArrayList tempList, int[] nums) {

        if (tempList.size() == nums.length){
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
