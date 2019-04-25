---
Time：2019/4/25
Title:Binary Tree Inorder Traversal
Difficulty: Medium
Author:小鹿
---



## 题目：Binary Tree Inorder Traversal（二叉树中序遍历）

Given a binary tree, return the *inorder* traversal of its nodes' values.

> 给定一个二叉树，返回它的*中序* 遍历。 

**Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

> **进阶:** 递归算法很简单，你可以通过迭代算法完成吗？ 



## solve:

###### ▉ 问题分析



###### ▉ 算法思路



###### ▉ 递归实现

```javascript
var inorderTraversal = function(root) {
    let arr = []
    
    const inorder = root =>{
        if(root == null) return null;
        inorder(root.left)
        arr.push(root.val)
        inorder(root.right)
    }
    inorder(root)
    return arr
};
```



###### ▉ 迭代实现

```

```

















