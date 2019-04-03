---
Time：2019/4/1
Title:Two Sum
Difficulty: simple
Author:小鹿
---



#### 题目一：Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:** 

```javascript
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1]
```



**Solve:**

###### ▉  法一：暴力破解法

> 算法思路：用目标值减去数组中的某一个数值，查找差值是否在数组中存在。

```javascript
/**
 * 步骤：
 * 1）外循环：target 值要一一减去数组中的元素，记录差值
 * 2）内循环：拿着差值去数组中比较判断是否存在
 * 3）如果存在：返回两个元素的下标
 * 4）如果不存在：继续遍历
 *
 * 性能分析：
 * 1）时间复杂度分析：两层 for 循环,所以时间复杂度为 O（n^2）
 * 2）空间复杂度分析：不需要额外的空间，所以空间复杂度为 O（1）
 */
var twoSum = function(nums, target) {
    for(let j = 0;j < nums.length; j++){
        subtract = target - nums[j];
        for(let i = 0;i < nums.length; i++){
            if(nums[i] == subtract && i !== j){
                return [j,i]
            }else{
                continue;
            }
        }
    }
    return false;
};
//测试
const nums = [2,7,11,15];
console.log(twoSum(nums,26));
```



###### ▉  法二：两遍哈希表

> 算法思路：先遍历数组将下标对应的元素存到散列表，然后同目标值减去的值去散列表中查看是否存在。

```javascript
/**
 * 步骤：
 * 1）遍历数组数据，将根据下标和元素值存放到散列表中。
 * 2）目标值减去数组元素差值并在散列表中查找。
 * 3）如果存在，返回两元素的下标。
 * 4）不存在继续遍历
 *
 * 性能分析：
 * 1）时间复杂度分析：随机访问的时间复杂度为O（1），但是需要遍历所有数据，所以时间复杂度为 O（n）。
 * 2）空间复杂度分析：需要额外的 n 大小的空间存储散列表，空间复杂度为 O(n)。
 */
var twoSum = function(nums, target) {
    var map = new Map();
    for(let i = 0;i < nums.length; i++){
        map.set(nums[i],i)
    }
    for (let j = 0; j < nums.length; j++) {
        substra = target - nums[j];
        if(map.has(substra) && map.get(substra) !== j){
            return [j,map.get(substra)]
        }
    }
}

// 测试
const nums = [2,7,11,15];
console.log(twoSum(nums,9));
```



###### ▉  法三：一遍哈希表

> 算法思路：遍历目标值减去数组元素的差值同时判断该值在散列表中是否存在差值，如果存在，则返回；否则将数据加入到散列表中。

```javascript
/**
 * 步骤：
 * 1）遍历目标值减去数组元素的差值同时判断该值在散列表中是否存在差值
 * 2）存在该差值，返回该元素下标
 * 3）不存在，将该差值存储到散列表中继续遍历。
 *
 * 性能分析：
 * 1）时间复杂度分析：随机访问的时间复杂度为O（1），但是需要遍历所有数据，所以时间复杂度为 O（n）。
 * 2）空间复杂度分析：需要额外的 n 大小的空间存储散列表，空间复杂度为 O(n)。
 */
var twoSum = function(nums, target) {
    var map = new Map();
    for(let i = 0;i < nums.length; i++){
        substra = target - nums[i];
        if(map.has(substra)){
            return [i,map.get(substra)]
        }
        map.set(nums[i],i)
    }
    return false;
}

// 测试
const nums = [2,7,11,15];
console.log(twoSum(nums,26));
```



###### ▉ 总结：

> 1、涉及到查找、判断是否存在，相关的数据结构有**散列表**、平衡二叉树、二分查找、跳表、二叉查找树。
>
> 2、使用数据结构的时候注意**适用条件**。
>
> 3、注意对时间复杂度、空间复杂度的优化策略。









