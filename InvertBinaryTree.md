---
Time：2019/4/21
Title: Invert Binary Tree
Difficulty: Easy
Author: 小鹿
---



## 题目：Invert Binary Tree（反转二叉树）

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





###### ▉ 算法思路





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























