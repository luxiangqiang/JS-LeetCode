---
Time：2019/4/4
Title: Majority Element 1
Difficulty: easy
Author: 小鹿
---



#### 题目：Majority Element 1

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋`times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

**Example 2:**

```
Input: [2,2,1,1,1,2,2]
Output: 2
```



#### solve:

###### ▉ 算法思路：摩尔投票算法

> 题目的要求是让我们求数组中超过一半数据以上相同的元素且总是存在的。有这样一个思路要和大家分享：
>
> 假如有这样一种数据，数组中的所存在的这个超过 n/2 以上的数据（众数）肯定比与此众数不相同的其他元素个数要多（n/2 以上）。我们可以这样统计，用一个变量来计数，另一个变量记录计数的该元素，遍历整个数组，如果遇到相同的 count 加 +1，不同的就  -1 ，最后所存储的就是众数，因为其他数据的个数比众数个数要少嘛，这就是所谓的**摩尔投票算法**。



###### ▉ 代码实现：

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    //用来计数相同的数据
    let count = 0;
    //存储当前的元素
    let majority = 0;
	//遍历整个数组
    for(let i = 0;i < nums.length; ++i){
        //如果 count 为 0 
        if(count === 0){
            //将当前数据为众数
            majority = nums[i];
            count++;
        }else if(majority === nums[i]){
            //如果遍历的当前数据与存储的当前数据相同，计数+1
            count++;
        }else{
            //若不相同，计数 - 1
            count--;
        }
    }
     //假设相同的众数呢？
    if(count === 0){
        return -1;
    }else{
        return majority;
    }
};
```





































