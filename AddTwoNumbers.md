---
​---
Time：2019/4/2
Title:ADD Two Numbers
Difficulty: medium
Author:小鹿
​---
---

#### 题目二：ADD Two Numbers

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```



**Solve:** 

###### ▉ 算法思路：

> 1）观察 Example 规律，关联到链表，用一个带头的链表存储。
>
> 2）多位数加多位数，反转链表转化整数，如果整数相加，可能会溢出，此方法行不通。
>
> 3）直接进行位数运算，两链表每取出一个就做运算，将结果放入到新链表中。

###### ▉ 临界条件：

> 1）一个链表比另一个链表长；
>
> 2）其中一个链表为 null。
>
> 3）求和运算会出现额外的进位（一般进位与最高位进位两种情况）。

###### ▉ 步骤：

> 1）遍历链表之前，要定义一个哨兵结点、临时结点、存储计算结果的结点、进位标志；
>
> 2）开始遍历数据，判断当前结点是否为 null，为 null 就用 0 代替，否则取出数值；
>
> 3）求和（加 carray 进位），判断是否进位？记录进位值；
>
> 4）求模取余，计算两位数的各位数存储到链表中，指针向后移动；
>
> 5）判断结点是否为 null，继续遍历（如果链表 l2 比 l1 短,没有下一结点只能返回本身下次处理当做 null 处理）
>
> 6) 退出 while 循环勿忘最高位满位情况,carray 还存放着 1,所以判断最高位是否需要进位，存放到链表最后

###### ▉ 代码实现：

```javascript
/**
 * 性能分析：
 * 1)遍历整个链表，时间复杂度为 O（n）。
 * 2)需要额外的 n 大小的空间存储 计算结果结点，空间复杂度为 O(n)。
 */
var addTwoNumbers = function(l1, l2) {
    //定义哨兵结点
    let head = new ListNode("head");
    let current = head;//临时指针
    //存储计算后的链表
    let sumNode = head;
    //定义进位变量
    let carray = 0;
    //开始遍历两个链表取数据，判断链表是否为 null
    while(l1 !== null || l2 !== null){
        //判断取数据的链表是否为nulL,为 null 就用 0 替换
        let num1 = 0;
        let num2 = 0;
        if(l1 == null){
            num1 = 0;
        }else{
            num1 = l1.val;
        }
        if(l2 == null){
            num2 = 0;
        }else{
            num2 = l2.val;
        }
        // let num1 = l1 == null ? 0 : l1.val;
        // let num2 = l2 == null ? 0 : l2.val;
        //计算取出的两个数值的和用于判断是否满进位，如果满 10,carray 需要记录进位,默认为 0
        let sum = num1 + num2 + carray;
        //判断是否需要存储进位值 1
        if(sum > 9){
           carray = 1;
        }else{
            carray = 0;
        }
        //carray = sum > 9 ? 1 : 0;
        //将两数之和相加[取模(取余运算)]添加到 sumNode 新链表中,一次排列
        current.next = new ListNode(sum % 10)
        //将指针指向下一链表结点
        current = current.next;
        //继续遍历链表中的数据，判断下一结点是否为 null
        if(l1 !== null){
            l1 = l1.next;
        }else{
            //如果链表 l1 比 l2 短,没有下一结点只能返回本身下次处理当做 null 处理
            l1 = l1;
        }
        if(l2 !== null){
            l2 = l2.next;
        }else{
            //如果链表 l2 比 l1 短,没有下一结点只能返回本身下次处理当做 null 处理
            l2 = l2;
        }
        // l1 为不为 null 才满足条件
        // l1 = l1 ? l1.next : l1;
        // l2 = l2 ? l2.next : l2;
    }
    //最高位满位情况,carray 还存放着 1,所以判断最高位是否需要进位
    if(carray === 1){
        //有哨兵的，所以需要 next 才能存放下一结点
        current.next = new ListNode(1);
    }
    //返回哨兵结点之后的链表
    return head.next;
}
```

###### ▉ 代码缩减:

```javascript
var addTwoNumbers = function(l1, l2) {
    //定义哨兵结点
    let head = new ListNode("head");
    let current = head;//临时指针
    //存储计算后的链表
    let sumNode = head;
    //定义进位变量
    let carray = 0;
    //开始遍历两个链表取数据，判断链表是否为 null
    while(l1 !== null || l2 !== null){
        //判断取数据的链表是否为nulL,为 null 就用 0 替换
        let num1 = l1 == null ? 0 : l1.val;
        let num2 = l2 == null ? 0 : l2.val;
        //计算取出的两个数值的和用于判断是否满进位，如果满 10,carray 需要记录进位,默认为 0
        let sum = num1 + num2 + carray;
        //判断是否需要存储进位值 1
        if(sum > 9){
           carray = 1;
        }else{
            carray = 0;
        }
        //carray = sum > 9 ? 1 : 0;
        //将两数之和相加[取模(取余运算)]添加到 sumNode 新链表中,一次排列
        current.next = new ListNode(sum % 10)
        //将指针指向下一链表结点
        current = current.next;
        //继续遍历链表中的数据，判断下一结点是否为 null
        l1 为不为 null 才满足条件
        l1 = l1 ? l1.next : l1;
        l2 = l2 ? l2.next : l2;
    }
    //最高位满位情况,carray 还存放着 1,所以判断最高位是否需要进位
    if(carray === 1){
        //有哨兵的，所以需要 next 才能存放下一结点
        current.next = new ListNode(1);
    }
    //返回哨兵结点之后的链表
    return head.next;
}
```



###### ▉ 总结：需要注意几点。

> 1、` l1 = l1 ? l1.next : l1` 代表的是 l1 不等于 null 会去 l1.next 的值。
>
> 2、用到哨兵思想，所以注意当前的指针指向。
>
> 3、两位数取模运算。



###### ▉ 扩展：

> 三位数怎么取得各个位置上的数字？（水仙花数）
>
> **答：**

```javascript
//移动小数点向前一位，得到小数点后一位
个位：a = 123 % 10 = 3
//移动小数点向前两位，得到小数点后两位，除以10取整
十位：b  = parseInt((123 % 100) / 10)
//移动小数点向前三位，得到小数点后三位，除以100取整
百位:：c = parseInt((123 % 1000) / 100)
//依次类推.....
```

