---
title: Daily Leetcode - 394 Decode String
description: Medium Stack
date: 2023-12-18 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 394. Decode String



### My Code

```java
class Solution {
    public String decodeString(String s) {
        Stack<String> strStack = new Stack<>();
        Stack<Integer> numStack = new Stack<>();
        StringBuilder currentString = new StringBuilder();
        int num = 0;

        for(char c: s.toCharArray()) {
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            } else if (c == '[') {
                numStack.push(num);
                strStack.push(currentString.toString());
                num = 0;
                currentString = new StringBuilder();
            } else if (c == ']') {
                StringBuilder temp = new StringBuilder(strStack.pop());//從 strStack 彈出一個，
                int repeatTimes = numStack.pop();
                for (int i = 0; i < repeatTimes; i++) {
                    temp.append(currentString);
                }
                currentString = temp;
            } else {
                currentString.append(c);
            }
        }
        return currentString.toString();
    }
}

```

目標是解碼這個字串，根據編碼規則將其轉換成 "accaccacc"。 以下是如何使用程式碼來達到這個目的：

* 初始化：

    numStack 和 strStack 都是空的。
    currentString 是空的。
    num 是 0。

* 遍歷字串：

遇到 '3'，num 變成 3。
遇到 '['，將 num（3）推入 numStack，將 currentString（空）推入 strStack，重置 num 和 currentString。
遇到 'a'，currentString 變成 "a"。
遇到 '2'，num 變成 2。
遇到 '['，將 num（2）推入 numStack，將 currentString（"a"）推入 strStack，重置 num 和 currentString。
遇到 'c'，currentString 變成 "c"。
遇到 ']'，numStack.pop() 是 2，strStack.pop() 是 "a"。 將 "c" 重複 2 次，得到 "cc"，然後拼接到 "a" 上，currentString 變成 "acc"。
遇到 ']'，numStack.pop() 是 3，strStack.pop() 是空。 將 "acc" 重複 3 次，得到 "accaccacc"。
最終結果：

遍歷結束，currentString 是 "accaccacc"，這是解碼後的字串。
在整個過程中，兩個堆疊 numStack 和 strStack 起到了關鍵作用。 每當遇到 '['，就會將當前的重複次數和字串保存起來，然後重置這些變數以準備解析下一個括號內的字串。 每當遇到 ']'，就會從堆疊中恢復先前儲存的重複次數和字串，並根據重複次數將當前字串重複並拼接，直到整個字串被完全解析。

```java
class Res {
    StringBuilder sb;
    int end;
    Res(int end) {
        this.sb = new StringBuilder();
        this.end = end;
    }
}

class Solution {
    private Res solve(String s, int idx) {
        int n = s.length();
        StringBuilder str = new StringBuilder();
        StringBuilder numSb = new StringBuilder();
        Res ans = new Res(idx);
        int i = idx;
        while (i < n) {
            char c = s.charAt(i);
            if (c == '[') {
                Res res = solve(s,i+1);
                int num = Integer.parseInt(numSb.toString());
                for (int j = 0; j < num; ++j) {
                    ans.sb.append(res.sb);
                }
                i = res.end+1;
                numSb = new StringBuilder();
            } else if (c == ']') {
                // ans.sb.append(str);
                ans.end = i;
                break;
            } else if (c >= '0' && c <= '9') {
                numSb.append(c);
                ++i;
            } else {
                ans.sb.append(c);
                ++i;
            }
        }
        return ans;
    }

    public String decodeString(String s) {
        return solve(s,0).sb.toString();
    }
}
```