---
Time：2019/4/5
Title: Majority Element 2
Difficulty: medium
Author: 小鹿
---



#### 问题：Majority Element 2 

Given an integer array of size *n*, find all elements that appear more than `⌊ n/3 ⌋` times.

**Note:** The algorithm should run in linear time and in O(1) space.

**Example 1:**

```
Input: [3,2,3]
Output: [3]
```

**Example 2:**

```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```



#### solve:

###### ▉ 算法思路：

> 1、上一篇是一个求超过 n/2 个数的数，采取的是用一个计数变量和计数元素变量来完成的。本篇题目是超过 n/3 的个数， 我们分别用两个变量来完成，**条件限制是时间复杂度是O(n),空间复杂度为O(1)**。
>
> 2、继续使用摩投票算法，假设要投票，选取票数超过 n/3 以上选为候选人，一个 n 被分为三等份，也就是说最多有两位当选人。
>
> 3、假设第一个人投甲，第二个投乙，甲、乙都站到台上各个计数为 1 ，随之第三个投甲，第四个投乙，计数分别加 1 ，第五个投丙，因为只有两个台子，所以那就让甲乙票数计数各减 1 ，当甲、乙的票数分别减到 0 之后，第  m 个人投丙，就让丙代替甲或已，继续遍历数据，直到遍历完成为止。
>
> 4、上述只选择出了那些有可能满足条件的数据，下面对cm、cn存储的数据做验证。



###### ▉ 其他解法：

> 如果没有题目中时间复杂度和空间复杂度的限制，有多种解决方法：
>
> **1、散列表解决：**先遍历一遍数据，统计每个数字出现的次数，然后再遍历一遍散列表，找出满足条件的数字。时间复杂度为O(n)，空间复杂度为 O(n)。
>
> **2、排序解决：**先进行一次排序（快排），然后遍历数据，找出满足条件的数据。时间复杂度为O(nlogn)，空间复杂度为O(1)。



###### ▉ 代码实现：

```javascript
  /**
    * @param {number[]} nums
    * @return {number[]}
    */
var majorityElement = function(nums) {
    let [m,n,cm,cn,countm,countn] = [0,0,0,0,0,0];
    let result = [];
    
    for(let i = 0;i < nums.length; ++i){
		//m === nums[i]和n === nums[i]的判断一定放到 cm === 0 和 cn === 0 之前，负责产生 bug。
        if(m === nums[i]){
            cm ++;
        }else if(n === nums[i]){
            cn ++;
        }else if(cm === 0){
            m = nums[i];
            cm ++;
        }else if(cn === 0){
            n = nums[i];
            cn ++;
        }else{
            cn--;
            cm--;
        }
    }
    //验证 cm、cn 存储的数据
    for(let index in nums){
        if(nums[index] === m){
            ++countm;
        }
        if(nums[index] === n){
            ++countn;
        }
    }
    
    if(countm > Math.floor(nums.length/3)){
        result.push(m);
    }

    if(countn > Math.floor(nums.length/3) && n != m){
        result.push(n);
    }
    return result;
};

//测试
let arr =[1,2,2,3,2,1,1,3];
console.log(majorityElement(arr));
```



























