---
Time：2019/4/10
Title: Merge K Sorted Lists
Difficulty: Difficulty
Author: 小鹿
---



## 题目：Merge K Sorted Lists

Merge *k* sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

> 合并 *k* 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。 

**Example:**

```javascript
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```



## Solve:

#### ▉ 算法思路

> 如果我们完成了简单的基于两个单链表的合并之后，对于这个题来说，考察点是分治算法，我认为还有一个考察点就是递归调用，分治的同时经常用递归来解决。
>
> 1、本道题可以借助归并排序的思想，稍加改造就可以解决。
>
> 2、将数组中的链表分治，就是不断的将数组中的链表中间划分，分别合并，然后整体合并成一个大链表。



#### ▉ 代码实现

```javascript
/**
  * @param {number[]} nums
  * @return {number[]}
  * 功能：合并 k 个链表
  * 边界条件：
  * 1）判断数组是否为空
  * 2）判断数组长度为 1 时
  * 3）判断数组长度为 2 时
  * 4）判断数组长度大于 2 时
  */
var mergeKLists = function(lists) {
    // 当 lists 中有一个链表时
    if(lists.length == 0){
        return null;
    }else if(lists.length == 1){
        // 判断数组长度为 1 时
        return lists[0];
    }else if(lists.length == 2){
        // 判断数组长度为 2 时
        return mergeTwoLists(lists[0],lists[1]);
    }else{
        // 判断数组长度大于 2 时
        // 取数组的中部坐标
        let middle = Math.floor(lists.length/2);
        // 取左右两边数组
        let leftList = lists.slice(0,middle);
        let rightList = lists.slice(middle);
		// 递归、分割、合并
        return mergeTwoLists(mergeKLists(leftList),mergeKLists(rightList));
    }       
};
//两个链表合并
var mergeTwoLists = function(l1, l2) {
    let result = null;

    //终止条件
    if(l1 == null) return l2;
    if(l2 == null) return l1;

    //判断数值大小递归
    if(l1.val < l2.val){
        result = l1;
        result.next = mergeTwoLists(l1.next,l2);
    }else{
        result = l2;
        result.next = mergeTwoLists(l2.next,l1);
    }
    
    //返回结果
    return result;
};   
```



#### ▉ 扩展：分治算法

> 分治算法经常和递归一块使用，所谓分治算法，顾名思义，分而治之，最基本的分之算法在归并排序、快速排序都有用到。也就是将原问题划分成 n 个规模较小，并且结构与原问题相似的子问题，递归地解决这些子问题，然后再合并其结果，就得到原问题的解。 



##### 1、分治算法递归每层操作

- 分解：将原问题分解成一系列的子问题。
- 解决：递归地求解各个子问题，若子问题足够小，则直接求解；
- 合并：将子问题的结果合并成原问题。



##### 2、分治算法满足的条件

- **可分解：**原问题与分解成的小问题具有相同的模式；
- **无关联：**原问题分解成的子问题可以独立求解，子问题之间没有相关性，这一点是分治算法跟动态规划的明显区别。
- **终止条件：**具有分解终止条件；
- **合并不能太复杂：**可以将子问题合并成原问题，而这个合并操作的复杂度不能太高，否则就起不到减小算法总体复杂度的效果了。









