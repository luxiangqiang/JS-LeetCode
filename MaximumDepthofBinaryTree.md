---
Time：2019/4/22
Title: Maximum Depth of Binary Tree
Difficulty: Medium
Author:小鹿
---



## 题目：Maximum Depth of Binary Tree（二叉树的最大深度）

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

> 给定一个二叉树，找出其最大深度。
>
> 二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
>
> **说明:** 叶子节点是指没有子节点的节点。

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.



## Solve：

###### ▉ 算法思路



###### ▉ 代码实现

```javascript
var maxDepth = function(root) {
   return root === null ? 0 : Math.max(maxDepth(root.left),maxDepth(root.right)) + 1; 
};
```





































