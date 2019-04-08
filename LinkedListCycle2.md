---
Time：2019/4/8
Title: Linked List Cycle II
Difficulty: medium
Author:小鹿
---



#### 题目：Linked List Cycle II

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

**Note:** Do not modify the linked list.

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**说明：**不允许修改给定的链表。

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

**Follow up**:
Can you solve it without using extra space?



#### Solve:

###### ▉ 算法思路：

> 题目要求返回单链表中存在循环链表的位置。
>
> 1、首先，先判断该单链表是否存在循环链表？用两个快慢指针（fast、slow）分别指向链表的头部，fast 每次移动两步，slow 每次移动一步，fast 移动的步数是 slow 的两倍。
>
> 2、当 slow 与 fast 发生重合的时候，则存在链表。（slow 遍历完单链表一遍，fast 遍历了单链表两遍，2 倍的关系，如果 pos = 0 时，正好在头结点重合）。
>
> 3、如果 pos > 0 的时候。也就是说单链表中存在环，slow 到与 fast 指针重合的地方走过的路径为 n，fast 走过的路径是 slow 的两倍也就是 2n 。如果此时让 fast 每次走一步，走 n 步之后还会回到重合点。
>
> 4、那么怎么知道环接入的位置呢？这里稍微用的到点数学知识，看下图：
>
> 当 fast 指针和 slow 指针重合时，我们在声明一个 q 指针来计算到环结点的距离，因为 fast 改为每次移动一步，且 q 也要移动一步，fast 与 q 重合的地方就是环的接入点。（因为 slow 走过的路径和 fast 走过的路径相同，其中不重合的地方就是接入点）

![](/images/LinkedListCycle.png)

![](/images/LinkedListCycle2.png)

###### ▉ 代码实现：

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
 * @return {ListNode}
 */
var detectCycle = function(head) {
    //判断头结点是否为 null
    if(head == null || head.next == null){
        return null;
    }
    let fast = head;
    let slow = head;
    while(fast !== null && fast.next !== null){
        fast = fast.next.next;
        slow = slow.next;
        //查找接入点
        if(fast == slow){
            slow = head;
            while(slow !== fast){
                fast = fast.next;
                slow = slow.next;
            }
            return  slow;
        }
    }
    return null;
};
```



























