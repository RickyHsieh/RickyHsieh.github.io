---
title: Daily Leetcode 20. Valid Parentheses
description: Easy 關於Stack
date: 2023-12-08 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

### 關於 stack 特性

* 先進後出
* Push(): Adds an element to the top of the stack.
* Pop(): Removes and returns the top element of the stack.
* Peek(): Returns the top element of the stack without removing it from the stack.
* isEmpty(): Check whether the stack is empty.

### 20. Valid Parentheses

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 
### 想法

### My Code

```java
import java.util.Stack;

public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                char top = stack.pop();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }
}

```