---
title: Daily Leetcode 144. Binary Tree Preorder Traversal
description: Easy 關於 BST preorder、inorder、postorder traversal
date: 2023-12-09 00:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge

### 相似題目

94. Binary Tree Inorder Traversal
145. Binary Tree Postorder Traversal
144. Binary Tree Preorder Traversal
 
### preorder、postorder、inorder traversal 特性

* 前序 Preorder : root -> left -> right
* 後序 Postorder : left -> right -> root
* 中序 InOrder : right -> left -> right

### My Code

#### 94. Binary Tree Inorder Traversal

* 中序 InOrder : right -> left -> right
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
    public List<Integer> inorderTraversal(TreeNode root) {
        //root.left - > root -> root.right
        List<Integer> result = new ArrayList<>();
        inorderTraversal(root, result);
        return result;
    }

        private void inorderTraversal(TreeNode node, List<Integer> result) {
        if (node == null) return;

        if (node.left != null) {
            inorderTraversal(node.left, result);
        }

        result.add(node.val);

        if (node.right != null) {
            inorderTraversal(node.right, result);
        }
    }
}
```

#### 144. Binary Tree Preorder Traversal
* 前序 Preorder : root -> left -> right
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
    public List<Integer> preorderTraversal(TreeNode root) {
        
        List<Integer> result = new ArrayList<>();
        preorderTraversal(result, root);
        return result;
    }

    public void preorderTraversal(List<Integer> result, TreeNode node) {
        
        if ( node == null) return;
        
        result.add(node.val);

        if (node.left != null) {
            preorderTraversal(result, node.left);
        }

        if(node.right != null) {
            preorderTraversal(result, node.right);
        }
    } 
}
```

#### 145. Binary Tree Postorder Traversal
* 後序 Postorder : left -> right -> root
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
    public List<Integer> postorderTraversal(TreeNode root) {
        
        List<Integer> result = new ArrayList<>();
        postorderTraversal(result, root);
        return result;
    }

    public void postorderTraversal(List<Integer> result, TreeNode node) {
        if (node == null) return;

        if (node.left != null) {
            postorderTraversal(result, node.left);
        }

        if (node.right != null) {
            postorderTraversal(result, node.right);
        }
        result.add(node.val);
    }
}
```