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

> 看到此题的入手点就是上方提出的三点二叉搜索树的三点要求：
>
> - 节点的左子树只包含**小于**当前节点的数。
> - 节点的右子树只包含**大于**当前节点的数。
> - 所有左子树和右子树自身必须也是二叉搜索树。
>
> 1）以上三点要求最容易解决的就是一个中序遍历，判断遍历出的每个元素后一个元素是否大于前一个元素，如果不符合条件，那么就不是一个二分搜索树。



###### ▉ 算法思路

> 1）定义全局的 boolean 变量，用来返回是否为 二叉搜索树。
>
> 2）定义一个边界值赋予 max 变量。每遍历一次，如果符合前后大小的要求，就将当前节点的值赋值给 max 变量，用于下一次遍历的结点的大小比较。如果不符合要求，我们将其布尔变量置为 false。
>
> 3）整个过程是用递归来解决的，在理解上还是有点不符合常规思路的。也是整个问题分析中最重要的一点。



###### ▉ 代码实现

```javascript
var isValidBST = function(root) {
    // boolean 变量
    let isValidBSTFlag = true;
    // 最大值变量
    let max = -Number.MAX_VALUE;
    const orderSearch = root => {
        // 终止条件（判断当前结点是否为 null）
        if (root) {
            // 中序遍历
            orderSearch(root.left);
            // 判断遍历前后的值是否逐渐升序
            if (root.val > max) {
                // 存储当前结点值，进行下一次比较
                max = root.val;
            } else {
                // 当前节点值小于前一结点值，返回 false
                isValidBSTFlag = false;
            }
            orderSearch(root.right);
        }
    }
    orderSearch(root);
    return isValidBSTFlag;
};
```













