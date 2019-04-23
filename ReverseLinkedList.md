---
Time：2019/4/23
Title: Reverse Linked List
Difficulty: Easy
Author: 小鹿
---



## 题目：Reverse Linked List（反转链表）

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?



## Solve:

###### ▉ 问题分析

> 1）反转链表的我们第一能够想到的方法就是最常用的方法，声明三个指针，把头结点变为尾结点，然后下一结点拼接到尾结点的头部，一次类推。说白了就是就是直接将链表指针反转就可以实现反转链表。



###### ▉ 算法思路

> 两种方法：
>
> - 一般反转
> - 递归法
>
> 一般解决：
>
> 1）定义三个指针，分别为 Pnext、pre、current，current 存储当前结点， pre 指向反转好的结点的头结点，Pnext 存储下一结点信息。
>
> 2）判断当前结点是否可以反转（是否为空链表或链表大于 1 个结点）?
>
> 步骤：
>
> 1）Pnext 指针存储下一结点 。
>
> 2）当前结点的 next 结点是否为 null (为 null 的话当前结点就是最后的一个结点)，如果为 null，将当前节点赋值为 head 头指针（断裂处）。
>
> 3）将 pre 指针指向的结点赋值当前节点 current 的下一结点 next。
>
> 4）然后让 pre 指针指向当前节点 current。
>
> 5）current 继续遍历, 当前节点指向 current 指向 Pnext。
>
> 递归法（重点分析）：
>
> 1）先确定终止条件：当下一结点为  null  时，返回当前节点；
>
> 2）判断当前的链表是否为  null；
>
> 3）递归找到尾结点，将其存储为头结点。
>
> 4）此时递归的层次是第二层递归，所以要设置为头结点的下一结点就是当前第二层结点，并且将第二节点的下一结点设置为 bull。



###### ▉ 测试用例

> 1）链表是空链表。
>
> 2）当前链表的长度小于等于 1。
>
> 3）输入长度大于 1 的链表。



###### ▉ 递归法

```javascript
const reverseList = (head)=>{
       if(head == null || head.next == null){
           return head;
       }else{
           let newhead = reverseList(head.next);
           head.next.next = head;
           head.next = null;
           return newhead;
       }
   }
```



###### ▉ 性能分析

> - 时间复杂度：O(n)。只需遍历整个链表就可以完成反转，时间复杂度为 O(n)。
> - 空间复杂度：O(1)。只需要常量级的空间，空间复杂度为 O(1)。









