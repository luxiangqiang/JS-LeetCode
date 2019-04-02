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

> 

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    let curEle = result = new ListNode(0)
    let carry = 0
    while (l1 || l2 || carry) {
        let sum = carry
        if (l1) {
            sum += l1.val
            l1 = l1.next
        }
        if (l2) {
            sum += l2.val
            l2 = l2.next
        }
        carry = sum > 9 ? 1 : 0
        curEle.next = new ListNode((sum) % 10)
        curEle = curEle.next
    }
    return result.next 
};
```

| 测试用例                               | 说明                                               |
| -------------------------------------- | -------------------------------------------------- |
| l1=[0,1]l1=[0,1]  l2=[0,1,2]l2=[0,1,2] | 当一个列表比另一个列表长时。                       |
| l1=[]l1=[]  l2=[0,1]l2=[0,1]           | 当一个列表为空时，即出现空列表。                   |
| l1=[9,9]l1=[9,9]  l2=[1]l2=[1]         | 求和运算最后可能出现额外的进位，这一点很容易被遗忘 |

