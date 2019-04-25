---
Time：2019/4/24
Title: Vaildata Binary Search Tree
Difficulty: Medium
Author: 小鹿
---



### 题目：Vaildata Binary Search Tree（验证二叉搜索树）

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

> 给定一个二叉树，判断其是否是一个有效的二叉搜索树。
>
> 假设一个二叉搜索树具有如下特征：
>
> - 节点的左子树只包含**小于**当前节点的数。
> - 节点的右子树只包含**大于**当前节点的数。
> - 所有左子树和右子树自身必须也是二叉搜索树。

**Example 1:**

```
Input:
    2
   / \
  1   3
Output: true
```

**Example 2:**

```
    5
   / \
  1   4
     / \
    3   6
Output: false
Explanation: The input is: [5,1,4,null,null,3,6]. The root node's value
             is 5 but its right child's value is 4.
```



## Solve:

###### ▉ 问题分析

> 



###### ▉ 算法思路

> 



###### ▉ 代码实现

```javascript
var isValidBST = function(root) {
    let isValidBSTFlag = true;
    let max = -Number.MAX_VALUE;
    const orderSearch = root => {
        if (root) {
            orderSearch(root.left);
            if (root.val > max) {
                max = root.val;
            } else {
                isValidBSTFlag = false;
            }
            orderSearch(root.right);
        }
    }
    orderSearch(root);
    return isValidBSTFlag;
};
```













