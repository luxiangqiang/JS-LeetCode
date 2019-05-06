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

> 1）二叉树的前、中、后遍历，首先明白前、中、后遍历的顺序是什么，对于二叉树的中序遍历来说，顺序是左子树节点 —> 根节点 —> 右子树节点。
>
> 2）通常递归的方法解决二叉树的遍历最方便不过，但是我还是喜欢增加点难度，用一般的迭代循环来实现。



###### ▉ 算法思路

> 递归法：
>
> 1）判断当前树是否为空。
>
> 2）递归树的左子树结点。
>
> 3）输出当前结点的值。
>
> 4）递归树的右子树节点。
>
> 迭代循环法：
>
> 1）声明一个栈，将树的左子节点入栈。
>
> 2）每出栈一个结点，输出当前结点的值，且将该结点的右子树进行遍历打印，保证每个出栈的结点输出值之后，再输出上一个左子节点之前，将当前结点的右子节点遍历毕。
>
> 3）整棵树遍历完毕的终止条件就是当前栈是否存在结点（树的左子节点）。



###### ▉ 递归实现

```javascript
var inorderTraversal = function(root) {
    let arr = []
    const inorder = root =>{
        // 判断当前的结点是否为空
        if(root == null) return null;
        // 递归左子树
        inorder(root.left)
        // 输出结点值
        arr.push(root.val)
        // 递归右子树
        inorder(root.right)
    }
    inorder(root)
    return arr
};
```



###### ▉ 迭代实现

```javascript
// 迭代实现二叉树的中序遍历
var inorderTraversal = function(root) {
    let stack = [];
    let result = [];

    while(true){
        // 判断树是否为空
        if(root == null) return result;

        // 先将树的左子节点推入栈中
        while(root !== null){
            stack.push(root);
            root = root.left;
        }

        // 遍历的终止条件
        if(stack.length !== 0){
            // 输出栈中的结点
            let temp = stack.pop();
            result.push(temp.val);
            // 如果当前存在右子节点，要先打印右子树节点
            root = temp.right;
        }else{
            break;
        }
    }
    return result;
}
```



###### ▉ 举一反三

> 1）试着分别写出前序遍历、后序遍历的递归实现和迭代实现代码。













