---
Time：2019/4/6
Title:First Missing Positive
Difficulty: Difficulty
Author:小鹿
---



#### 题目：First Missing Positive

Given an unsorted integer array, find the smallest missing positive integer. 

**Note:**

Your algorithm should run in *O*(*n*) time and uses constant extra space.

**Example 1:**

```
Input: [1,2,0]
Output: 3
```

**Example 2:**

```
Input: [3,4,-1,1]
Output: 2
```

**Example 3:**

```
Input: [7,8,9,11,12]
Output: 1
```



#### Solve：

###### ▉ 算法思路：

> 桶排序思想。
>
> 遍历第一遍数据，将数据存放到与下标相同的位置，遍历第二遍数据，判断每个下标对应的数据是否为下标值。如果不是，该数值就是当前确实的最小正整数;当数组遍历完还有没找到，那么数组的长度 + 1 就是缺失的最小正整数值。



###### ▉ 算法步骤：

> 1、把数组的每一个下标当做是一个桶，每个桶只能存放一个数据（每个下标对应一个数据），我们规定桶中的数据和下标的对应关系是 0 下标对应数据1,1下标对应数据2，2下标对应数据3......，题目要求我们在O(n)的时间复杂度内找出一组数据中缺失的最小正整数。
>
> 2、遍历第一遍数组中的数据，按照步骤 1 的规定，先判断两个当前下标对应的数据是否为规定的数据，如果不是，我们将该数据存放到规定的下标对应的数组中。然后交换的数据继续进行判断，直到该数据放到规定下标的数组中为止（小于等于 0 和 数据大于数组长度的除外）。
>
> 3、再遍历数组，从下标 0 开始判断该下标是否存放规定的数据，如果不是则该下标就是这组数据中缺失的最小正整数。
>
> 4、如果数组中的数据都匹配对应的下标，那么最小正整数就是数组长度加一。



###### ▉ 代码实现：

```javascript
/**
* @param {number[]} nums
* @return {number}
* 边界条件：
* 1) 判断传入的数组是否为空。 
* 2) 判断数组中的数据只有 1 个。
* 3) 交换数据时，判断相同数据的处理。
*/
var firstMissingPositive = function(nums) {
    //遍历数组
    for(let i = 0;i < nums.length;i++){
        //如果当前的数据不对应正确的下标 + 1 && 数据大于 0 && 长度小于等于数组
        while(nums[i] != i+1 && nums[i] > 0 && nums[i] <= nums.length){
            //判断该数据对应正确位置的数据是否相同
            if(nums[nums[i]-1] == nums[i]) {
                //如果相同，将该下标对应的元素置为 0
                nums[i] = 0;
                break;
            }
            //如果不重复，就交换数据
            let temp = nums[nums[i] - 1];
            nums[nums[i] - 1] = nums[i];
            nums[i] = temp;
        }
    }
    //遍历所有数据,找出缺失的最小正整数
    let index = 0;
    for(; index < nums.length; index++){
        if(nums[index] !== index+1){
            break;
        }
    }
    return index+1;
};

//测试
let arr =[];
console.log(firstMissingPositive(arr))
```



###### ▉ 总结：

> 1、桶排序的思想。
>
> 2、桶排序还可以实现在一组数据中查找重复的数据。



















