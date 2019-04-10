---
Time：2019/4/10
Title: Merge K Sorted Lists
Difficulty: Difficulty
Author: 小鹿
---



#### 题目：Merge K Sorted Lists

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



#### Solve:

###### ▉ 算法思路

> 如果我们完成了简单的基于两个单链表的合并之后，对于这个题来说，考察点是分治算法，我认为还有一个考察点就是递归调用，分治的同时经常用递归来解决。
>
> 1、本道题可以借助归并排序的思想，稍加改造就可以解决。
>
> 2、将数组中的链表分治，就是不断的将数组中的链表中间划分，分别合并，然后整体合并成一个大链表。



###### ▉ 代码实现

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





###### ▉ 扩展：递归

> 
>





###### ▉ 扩展：分治算法

> 