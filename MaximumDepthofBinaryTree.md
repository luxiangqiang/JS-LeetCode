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

###### ▉ 问题分析

> 求二叉树的最大深度，我们要知道树的深度怎么计算的？
>
> 1）树的深度，深度，顾名思义，从上到下，第一层为 1，每向下一层，深度 + 1。
>
> 2）观察上图，我们计算时，只需记录两个子树最深的结点为主。
>
> 3）求二叉树的深度，必然要用到递归来解决。



###### ▉ 算法思路

> 1）判断树是否为 null。
>
> 2）分别递归左右子树。
>
> 3）只计算叠加计数（递归最深）最大的数字。



###### ▉ 代码实现

```javascript
var maxDepth = function(root) {
    // 如果根节点为 null 
    if(root === null) return 0;
	// 递归左子树
    let depthLeft  = maxDepth(root.left);
    // 递归右子树
    let depthRight  = maxDepth(root.right);
	// 将子问题合并求总问题
    return Math.max(depthLeft,depthRight) + 1;
};
```

































