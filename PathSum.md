---
Time：2019/4/26
Title: Path Sum
Difficulty: Easy
Author: 小鹿
---



## 题目：Path Sum（路径总和）

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

###### ▉ 问题分析

> 1）搜索从根节点到叶子节点能够达到目标值，毋庸置疑，一看到检索二叉搜索树，就应该想起递归。
>
> 2）第一个想法就是一个个进行相加，将每条路径相加完成之后，判断是否达到当前目标值？
>
> 3）但是 （2）的解决方案的想法要用到递归上，需要转变一下思路，毕竟我们要用递归的编程技巧来解决，所以思维需要稍微转变一下（将问题化成子问题，子问题与总问题有相同的解决思路）。



###### ▉ 算法思路

> 1）既然要用到递归来解决，这样来想，每遍历一个结点，我们就用 sum 减去当前结点，然后问题就会变成从当前结点到叶子节点能够满足 sum 减去当前结点的值，那么就存在满足条件的路径。
>
> 2）在（1）中，将问题化成子问题，然后子问题和问题有相同的解决思路，那么就可以使用递归来解决。
>
> 3）用 flag 做标识，一旦满足路径之和等于目标值，就让改变 flag 的状态。



###### ▉ 代码实现

```javascript
 var hasPathSum = function(root, sum) {
     let flag = false;
     // 判断当前二叉树是否等于 null
     if(root == null) return false;

     dfs = (root,sum)=>{
         // 如果当前结点为 null ，返回 false
         if(root == null) return false;
         // 判断左右子树是否为 null
         if(root.left == null && root.right == null){
             // 如果不为 null，就判断当前的值和最后一个结点值是否相同
             if(sum == root.val){
                 flag = true;
                 return;
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



















