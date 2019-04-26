---
Time：2019/4/21
Title: Invert Binary Tree
Difficulty: Easy
Author: 小鹿
---



## 题目：Invert Binary Tree（翻转二叉树）

Invert a binary tree.

> 反转二叉树

**Example:**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```



## Solve:

###### ▉ 问题分析

> 由上图可以分析反转二叉树，只是对左右子树的数据进行交换，再仔细观察，并不是每个节点的左右子树进行交换，而是左子树的叶子节点和右子树的叶子节点进行交换，另外两个子节点进行交换，那我们不得不用到递归了。 



###### ▉ 算法思路

> 1）判断树是否为空（同时也是终止条件）。
>
> 2）左右子树结点交换。
>
> 3）分别对左右子树进行递归。



###### ▉ 代码实现

```javascript
var invertTree = function(root) {
    //判断当前树是否为 null
    if(root == null) return root;

    let right = root.right;
    let left = root.left;
    root.right = left;
    root.left = right;

    invertTree(left);
    invertTree(right); 
    return root;
};
```























