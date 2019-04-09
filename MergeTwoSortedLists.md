---
Time：2019/4/9
Title: Merge Two Sorted Lists
Difficulty: Easy
Author: 小鹿
---



#### 题目：Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```



#### Solve:

###### ▉ 算法思路

> 1、正常思路，循环遍历迭代比较大小，每取出一个数据，将小数据加入到额外的数组中去，直到比较完毕，将其中一个剩余的数组追加到额外的数组尾部。
>
> 2、递归思路。满足递归的三个条件：
>
> - 将问题能不能化为子问题去解决？
> - 子问题的解决方式是否和总问题相似？
> - 是否有终止条件？



###### ▉ 递归实现

```javascript
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



###### ▉ 递归缺点

> 有时候问题可以使用递归，但是由于递归的缺点会放弃使用。
>
> 1、递归警惕堆栈溢出。
>
> 2、警惕递归重复元素计算。
>
> 3、递归的高空间复杂度。



###### ▉ 怎么正确写出递归代码？

> 1、将问题化为子问题。
>
> 2、解决子问题。
>
> 3、寻找终止条件。
>
> 4、写出递归公式。
>
> 5、将递推公式转化为代码。