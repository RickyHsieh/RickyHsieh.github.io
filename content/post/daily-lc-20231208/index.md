---
title: Daily Leetcode 606. Construct String from Binary Tree
description: Easy 前序 preorder Traversal
date: 2023-12-07 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

### 606. Construct String from Binary Tree

Given the root of a binary tree, construct a string consisting of parenthesis and integers from a binary tree with the preorder traversal way, and return it.

Omit all the empty parenthesis pairs that do not affect the one-to-one mapping relationship between the string and the original binary tree.


### 想法

* 使用遞迴

* 第一版 : 一開始的方法是先找到點，再處理括號字串，犯了一個小錯誤，因為使用String，而沒有考慮到可能會劇烈的修改字串(插入括弧或值)，而造成效能低落，原因為我每次修改String，當我使用 + 算符來連接字串時，每次操作實際上都會創建一個新的字串，因為字串在 Java 中是不可變的。這會導致在連接大量字符串時性能降低。
改法 StringBuilder 可在不創建新對象的情況下添加或修改字串。


* 第二版 : 避免不必要的遞歸調用：在這個的實現中，即使左子樹或右子樹為 null，也會進行遞迴調用。可以通過直接檢查子節點是否為 null 來避免這些不必要的調用。
    直接使用 StringBuilder 進行遞歸：目前先遞迴並創建左右子樹的字串，然後再將它們添加到 StringBuilder。相反的，可以直接在遞歸函數中使用 StringBuilder，這樣可以避免創建額外的字串。

* 第三版(查別人的解法) :
定義為 static 可能會對性能有輕微的提升。這種性能提升（如果存在的話）的原因主要是與如何存取靜態方法相比於實例方法有關：

存取控制：靜態方法屬於類本身而不是類的實例。因此，它們不需要存取和操作對象的實例變量。這意味著調用靜態方法時不需要創建類的實例，這可能稍微減少了記憶體的使用和管理開銷。

內聯優化：在某些情況下，靜態方法可以更容易被JVM（Java虛擬機）進行內聯優化。內聯是一種優化，其中方法的內容直接插入到調用點，從而節省了方法調用的開銷。然而，這種優化也可能適用於非靜態方法，特別是在現代JVM實現中。

語義清晰：將方法定義為靜態的，意味著它不依賴於對象的內部狀態。這可以讓編譯器和JVM更容易進行一些優化，因為它們不需要關心對象狀態的變化。


### My Code

* 第一版
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public String tree2str(TreeNode root) {
        
        // preorder traversal way
       
        StringBuilder sb = new StringBuilder();
        String result = tree2sb(sb, root);
        return result;
    }

    public String tree2sb(StringBuilder sb, TreeNode root) {

      if (root == null) return "";
      sb.append(root.val);

      if (root.left != null || root.right != null) {
          sb.append("(");
          tree2sb(sb, root.left);
          sb.append(")");

          if (root.right != null) {
            sb.append("(");
            tree2sb(sb, root.right);
            sb.append(")");
          }
      }

      return sb.toString();

    }
}
```

* 第二版
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public String tree2str(TreeNode root) {
        
        // preorder traversal way
       
        StringBuilder sb = new StringBuilder();
        String result = tree2sb(sb, root);
        return result;
    }

    public String tree2sb(StringBuilder sb, TreeNode root) {

      if (root == null) return "";
      sb.append(root.val);

      if (root.left != null || root.right != null) {
          sb.append("(");
          tree2sb(sb, root.left);
          sb.append(")");

          if (root.right != null) {
            sb.append("(");
            tree2sb(sb, root.right);
            sb.append(")");
          }
      }

      return sb.toString();

    }
}
```

* 第三版
```java
class Solution {
    public String tree2str(TreeNode root) {
        // Using StringBuilder for efficient string concatenation
        StringBuilder sb = new StringBuilder();
        // Calling the helper method with StringBuilder and the root of the tree
        tree2sb(sb, root);
        // Converting the StringBuilder to a string and returning it
        return sb.toString();
    }

    public static void tree2sb(StringBuilder sb, TreeNode root) {
        // If the current node is null, return immediately
        if (root == null) return;

        // Append the value of the current node to the StringBuilder
        sb.append(root.val);

        // Check if parentheses are needed. Parentheses are added if either left or right child is not null
        if (root.left != null || root.right != null) {
            sb.append("(");
            // Recursively call for the left child
            tree2sb(sb, root.left);
            sb.append(")");

            // Process the right child, only if it's not null
            if (root.right != null) {
                sb.append("(");
                // Recursively call for the right child
                tree2sb(sb, root.right);
                sb.append(")");
            }
        }
    }
}

```

#### Complexity
時間複雜度：

這個方法執行了一次深度優先搜索（DFS）。
在遍歷過程中，每個節點被訪問一次且只一次。
因此，時間複雜度主要取決於樹中節點的總數。
如果樹中有 n 個節點，則時間複雜度是O(n)。
空間複雜度：

空間複雜度主要來自於遞歸調用的堆棧空間和 StringBuilder 的使用。
在最壞情況下（樹完全不平衡），遞歸的深度可以達到樹的高度，即O(n)。
但對於平衡的二叉樹，遞歸的深度是O(logn)。
StringBuilder 的空間複雜度取決於最終生成的字符串長度。由於結果字符串長度與樹中節點數量成正比，因此這部分的空間複雜度也是O(n)。
