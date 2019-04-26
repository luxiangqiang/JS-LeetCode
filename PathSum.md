---
Time：2019/4/26
Title: Path Sum
Difficulty: Easy
Author: 小鹿
---



## 题目：Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.

> 给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。
>
> **说明:** 叶子节点是指没有子节点的节点。
>
> **示例:** 
> 给定如下二叉树，以及目标和 `sum = 22`，

**Example:**

Given the below binary tree and `sum = 22`,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.



## Solve:

###### ▉ 代码实现

```javascript
 var hasPathSum = function(root, sum) {
     let flag = false;
     // 判断当前二叉树是否等于 null
     if(root == null) return false;

     dfs = (root,sum)=>{
         if(root == null) return false;
         if(root.left == null && root.right == null){
             if(sum == root.val){
                 flag = true;
             }
         }
		 // 递归搜索所有路径
         dfs(root.left,sum - root.val)
         dfs(root.right,sum - root.val)
     }
     dfs(root,sum)
     return flag;
 };
```



















