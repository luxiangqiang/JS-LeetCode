---
Time：2019/4/27
Title: Minimum Distance Between BST Nodes
Difficulty: Easy
Author: 小鹿
---



## 题目：Minimum Distance Between BST Nodes（二叉搜索树结点最小距离）

Given a Binary Search Tree (BST) with the root node `root`, return the minimum difference between the values of any two different nodes in the tree.

> 给定一个二叉搜索树的根结点 `root`, 返回树中任意两节点的差的最小值。 

**Example :**

```
Input: root = [4,2,6,1,3,null,null]
Output: 1
Explanation:
Note that root is a TreeNode object, not an array.

The given tree [4,2,6,1,3,null,null] is represented by the following diagram:

          4
        /   \
      2      6
     / \    
    1   3  

while the minimum difference in this tree is 1, it occurs between node 1 and node 2, also between node 3 and node 2.
```

**Note:**

1. The size of the BST will be between 2 and `100`.
2. The BST is always valid, each node's value is an integer, and each node's value is different.



## Solve:

###### ▉ 问题分析

> 返回树中任意两个节点的差值，根据问题，可以将问题理解为，每个任意节点的差值的绝对值，那怎么进行相减呢？还需要用到树中的中序遍历。



###### ▉ 算法思路

> 1）对树进行中序遍历，中序遍历的的值是逐渐递增的，我们将其遍历整棵树存入数组。
>
> 2）然后对数组中的前后两个数求差值，求的最小的差值为树中任意两点的差的最小值。



###### ▉ 代码实现

```javascript
var minDiffInBST = function(root) {
    if(root == null) return null;
    let arr = [];
    let min = Number.MAX_VALUE
	// 中序遍历
    distance = (root)=>{
        if(root == null) return null;
        distance(root.left)
        arr.push(root.val);
        distance(root.right)
    }
	
    distance(root);
    // 求差值
    for(let i = 1;i < arr.length;i++){
        min = Math.min(min,arr[i] - arr[i - 1])    
    } 
    return min;
};
```











♂