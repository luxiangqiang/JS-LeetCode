---
Time：2019/4/16
Title: Sliding Window Maximum
Difficulty: Difficulty
Author: 小鹿
---



## 题目：Sliding Window Maximum

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

> 给定一个数组 *nums*，有一个大小为 *k* 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口 *k* 内的数字。滑动窗口每次只向右移动一位。
>
> 返回滑动窗口最大值。

**Example:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**Note:** 
You may assume *k* is always valid, 1 ≤ k ≤ input array's size for non-empty array.

**Follow up:**
Could you solve it in linear time?



## Solve:

###### ▉ 问题分析

> 暴力破解法
>
> 1）看到这个题目最容易想到的就是暴力破解法，借助一个 for 循环，两个变量，整体移动窗口，然后每移动一次就在大小为 k 的窗口求出最大值。
>
> 2）但是这样的解决效率非常低，如果数据非常大时，共有 n1 个数据，窗口大小为 n2（n1 远远大于 n2），时间复杂度为 n2(n1 - n2) 。也就是 n1 * n2，最坏时间复杂度为 n^2。
>
> 优先级队列
>
> 1）每次移动窗口求最大值，以及在动态数据中求最大值，我们想到的就是优先级队列，而优先级队列的实现是堆这种数据结构，这道题用堆解决效率更高。如果对堆不熟悉，赶紧给自己补补功课吧！底部有我写的文章链接。
>
> 2）通过堆的优化，向堆中插入数据时间复杂度为 logn ，所以时间复杂度为 nlogn。



###### ▉ 算法思路

> 暴力破解法：
>
> 1）用两个指针，分别指向窗口的起始位置和终止位置，然后遍历窗口中的数据，求出最大值；向前移动两个指针，然后操作，直到遍历数据完成位置。
>
> 优先级队列：
>
> 1）需要维护大小为 k 的大顶堆，堆顶就是当前窗口最大的数据，当移动窗口时，如果插入的数据大于堆顶的数据，将其加入到结果集中。同时要删除数据，如果删除的数据为最大数据且插入的数据小于删除的数据时，向大小为 k 的以 logn 的时间复杂度插入，返回堆顶元素。



###### ▉ 暴力破解法

```javascript

var maxSlidingWindow = function(nums, k) {
    if(k > nums.length || k === 0) return [];
    let res = [], maxIndex = -1;
    for(let l = 0, r = k-1;r < nums.length;l++, r++){
        if(maxIndex < l){
            // 遍历求出最大值
            let index = l;
            for(let i = l;i <= r;i++) {
                if(nums[i] > nums[index]) index = i;
            }
            maxIndex = index;
        }
        if(nums[r] > nums[maxIndex]){
            maxIndex = r;
        }
        res.push(nums[maxIndex]);
    }
    return res;
};
```



###### ▉ 优先级队列

```javascript
let count = 0;
let heap = [];
let n = 0;
var maxSlidingWindow = function(nums, k) {
    let pos = k;
    n = k;
    let result = [];
    let len = nums.length;

    // 判断数组和最大窗口树是否为空
    if(nums.length === 0 || k === 0) return result;

    // 建大顶堆
    let j = 0
    for(;j < k; j++){
        insert(nums[j]);
    }
    result.push(heap[1]); 

    // 移动窗口
    while(len - pos > 0){
        if(nums[k] > heap[1]){
            result.push(nums[k]);
            insert(nums[k]);
            nums.shift();
            pos++; 
        }else{
            if(nums.shift() === heap[1]){
                removeMax(); 
            }
            insert(nums[k-1]);
            result.push(heap[1]);
            pos++;
        }
    }
    return result;
};  



// 插入数据
const insert = (data) =>{
    //判断堆满
    // if(count >= n) return; // >=

    // 插入到数组尾部
    count++
    heap[count] = data;

    //自下而上堆化
    let i = count;
    while(i / 2 > 0 && heap[i] > heap[parseInt(i/2)]){
        swap(heap,i,parseInt(i/2));
        i = parseInt(i/2);
    }
}

// 两个数组内元素交换
swap = (arr,x,y) =>{
    let temp = arr[x];
    arr[x] = arr[y];
    arr[y] = temp;
}

// 堆的删除
const removeMax = () =>{
    // 判断堆空
    if(count <= 0) return ;

    // 最大数据移到最后删除
    heap[1] = heap[count];

    // 长度减一
    count--;
    // 删除数据
    heap.pop();

    // 从上到下堆化
    heapify(heap,count,1);
}

// 从上到下堆化
const heapify = (heap,count,i) =>{
    while(true){
        // 存储堆子节点的最大值下标
        let maxPos = i;

        // 左子节点比父节点大
        if(i*2 < n && heap[i*2] > heap[i]) maxPos = i*2;
        // 右子节点比父节点大
        if(i*2+1 <= n && heap[i*2+1] > heap[maxPos]) maxPos = i*2+1;

        // 如果没有发生替换，则说明该堆只有一个结点（父节点）或子节点都小于父节点
        if(maxPos === i) break;

        // 交换
        swap(heap,maxPos,i);
        // 继续堆化
        i = maxPos;
    }
}
```



###### ▉ 性能分析

> 暴力破解法
>
> - 时间复杂度：O（n^2）.
> - 空间复杂度：O（1）.
>
> 优先级队列
>
> - 时间复杂度：nlogn.
> - 空间复杂度：O(1).



###### ▉ 扩展

> 堆：
>
> 1）堆插入、删除操作
>
> 2）如何实现一个堆？
>
> 3）堆排序
>
> 4）堆的应用

详细查看写的另一篇关于堆的文章：[数据结构与算法之美【堆】](http://luxiangqiang.xn--6qq986b3xl/2019/01/07/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E4%B8%8E%E7%AE%97%E6%B3%95%E4%B9%8B%E7%BE%8E%E3%80%90%E5%A0%86%E3%80%91/)













