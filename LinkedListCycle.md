---
Time：2019/4/7
Title: Linked List Cycle
Difficulty: Easy
Author:小鹿
---



#### 题目：Linked List Cycle I

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

**Follow up:**

Can you solve it using *O(1)* (i.e. constant) memory?



#### Slove:

###### ▉ 算法思路：

> 两种解题思路：
>
> 1）哈希表法：遍历链表，没遍历一个节点就要在哈希表中判断是否存在该结点，如果存在，则为环；否则，将该结点插入到哈希表中继续遍历。
>
> 2）用两个快慢指针，快指针走两步，慢指针走一步，如果快指针与慢指针重合了，则检测的当前链表为环；如果当前指针或下一指针为 null ，则链表不为环。



###### ▉ 方法一：哈希表

```javascript
   /**
        * Definition for singly-linked list.
        * function ListNode(val) {
        *     this.val = val;
        *     this.next = null;
        * }
        */
        /**
        * @param {ListNode} head
        * @return {boolean}
        */

        var hasCycle = function(head) {
            let fast = head;
            let map = new Map();
            while(fast !== null){
                if(map.has(fast)){
                    return true;
                }else{
                    map.set(fast);
                    fast = fast.next;
                }
            }
            return false;
        };

```



###### ▉ 方法二：快慢指针

```javascript
 var hasCycle = function(head) {
     if(head == null || head.next == null){
     	return false;
     }
     let fast = head.next;
     let slow = head;
     while(slow != fast){
         if(fast == null || fast.next == null){
         	return false;
     	 }
         slow = slow.next;
         fast = fast.next.next;
     }
     return true;
 };
```



###### ▉ 方法二：快慢指针

> 这部分代码是我自己写的，和上边的快慢指针思路相同，运行结果相同，但是当运行在 leetcode 时，就会提示超出时间限制，仔细对比代码，我们可以发现，在逻辑顺序上还是存在差别的，之所以超出时间限制，是因为代码的运行耗时长。

```javascript
//超出时间限制
var hasCycle = function(head) {
    if(head == null || head.next == null){
    	return false;
    }
    let fast = head.next;
    let slow = head;
    while(fast !== null && fast.next !== null){
        if(slow === fast) return true;
        slow = head.next;
        fast = fast.next.next;
    }
	return false;
};
```

