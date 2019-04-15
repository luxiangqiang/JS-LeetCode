---
Time：2019/4/15
Title: Design Circular Deque
Difficulty: Medium
Author: 小鹿
---



## 题目：Design Circular Deque

Design your implementation of the circular double-ended queue (deque).

Your implementation should support following operations:

- `MyCircularDeque(k)`: Constructor, set the size of the deque to be k.
- `insertFront()`: Adds an item at the front of Deque. Return true if the operation is successful.
- `insertLast()`: Adds an item at the rear of Deque. Return true if the operation is successful.
- `deleteFront()`: Deletes an item from the front of Deque. Return true if the operation is successful.
- `deleteLast()`: Deletes an item from the rear of Deque. Return true if the operation is successful.
- `getFront()`: Gets the front item from the Deque. If the deque is empty, return -1.
- `getRear()`: Gets the last item from Deque. If the deque is empty, return -1.
- `isEmpty()`: Checks whether Deque is empty or not. 
- `isFull()`: Checks whether Deque is full or not.

> 设计实现双端队列。
> 你的实现需要支持以下操作：
>
> - MyCircularDeque(k)：构造函数,双端队列的大小为k。
> - insertFront()：将一个元素添加到双端队列头部。 如果操作成功返回 true。
> - insertLast()：将一个元素添加到双端队列尾部。如果操作成功返回 true。
> - deleteFront()：从双端队列头部删除一个元素。 如果操作成功返回 true。
> - deleteLast()：从双端队列尾部删除一个元素。如果操作成功返回 true。
> - getFront()：从双端队列头部获得一个元素。如果双端队列为空，返回 -1。
> - getRear()：获得双端队列的最后一个元素。 如果双端队列为空，返回 -1。
> - isEmpty()：检查双端队列是否为空。
> - isFull()：检查双端队列是否满了。

**Example:**

```
MyCircularDeque circularDeque = new MycircularDeque(3); // set the size to be 3
circularDeque.insertLast(1);			// return true
circularDeque.insertLast(2);			// return true
circularDeque.insertFront(3);			// return true
circularDeque.insertFront(4);			// return false, the queue is full
circularDeque.getRear();  			// return 2
circularDeque.isFull();				// return true
circularDeque.deleteLast();			// return true
circularDeque.insertFront(4);			// return true
circularDeque.getFront();			// return 4
```

 

**Note:**

- All values will be in the range of [0, 1000].
- The number of operations will be in the range of [1, 1000].
- Please do not use the built-in Deque library.



## Solve:

###### ▉ 算法思路

> 借助 Javascript 中数组中的 API 可快速实现一个双向队列。



###### ▉ 代码实现

```javascript
 //双端列表构造
        var MyCircularDeque = function(k) {
            this.deque = [];
            this.size = k;
        };

        /**
        * Adds an item at the front of Deque. Return true if the operation is successful. 
        * @param {number} value
        * @return {boolean}
        */
        MyCircularDeque.prototype.insertFront = function(value) {
            if(this.deque.length === this.size){
                return false;
            }else{
                this.deque.unshift(value);
                return true;
            }
        };

        /**
        * Adds an item at the rear of Deque. Return true if the operation is successful. 
        * @param {number} value
        * @return {boolean}
        */
        MyCircularDeque.prototype.insertLast = function(value) {
            if(this.deque.length === this.size){
                return false;
            }else{
                this.deque.push(value);
                return true;
            }
        };

        /**
        * Deletes an item from the front of Deque. Return true if the operation is successful.
        * @return {boolean}
        */
        MyCircularDeque.prototype.deleteFront = function() {
            if(this.deque.length === 0){
                return false;
            }else{
                this.deque.shift();
                return true;
            }
        };

        /**
        * Deletes an item from the rear of Deque. Return true if the operation is successful.
        * @return {boolean}
        */
        MyCircularDeque.prototype.deleteLast = function() {
            if(this.deque.length === 0){
                return false;
            }else{
                this.deque.pop();
                return true;
            }
        };

        /**
        * Get the front item from the deque.
        * @return {number}
        */
        MyCircularDeque.prototype.getFront = function() {
            if(this.deque.length === 0){
                return -1;
            }else{
                return this.deque[0];
            }
        };

        /**
        * Get the last item from the deque.
        * @return {number}
        */
        MyCircularDeque.prototype.getRear = function() {
            if(this.deque.length === 0){
                return -1;
            }else{
                return this.deque[this.deque.length - 1];
            }
        };

        /**
        * Checks whether the circular deque is empty or not.
        * @return {boolean}
        */
        MyCircularDeque.prototype.isEmpty = function() {
            if(this.deque.length === 0){
                return true;
            }else{
                return false;
            }
        };

        /**
        * Checks whether the circular deque is full or not.
        * @return {boolean}
        */
        MyCircularDeque.prototype.isFull = function() {
            if(this.deque.length === this.size){
                return true;
            }else{
                return false;
            }
        };

        //测试
        var obj = new MyCircularDeque(3)
        var param_1 = obj.insertFront(1)
        var param_2 = obj.insertLast(2)
        console.log('-----------------------------插入数据------------------------')
        console.log(`${param_1}${param_2}`)
        var param_3 = obj.deleteFront()
        var param_4 = obj.deleteLast()
        console.log('-----------------------------删除数据------------------------')
        console.log(`${param_3}${param_4}`)
        var param_5 = obj.getFront()
        var param_6 = obj.getRear()
        console.log('-----------------------------获取数据------------------------')
        console.log(`${param_5}${param_6}`)
        var param_7 = obj.isEmpty()
        var param_8 = obj.isFull()
        console.log('-----------------------------判断空/满------------------------')
        console.log(`${param_7}${param_8}`)
```



































