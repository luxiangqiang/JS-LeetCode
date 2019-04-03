---
Time：2019/4/3
Title:3Sum
Difficulty: medium
Author:小鹿
---



#### 题目三：ADD Two Numbers

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero. 

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



**Solve:** 

###### ▉ 代码实现：

```javascript
  /**
  * @param {number[]} nums
  * @return {number[][]}
  */

var threeSum = function(nums) {
    //用来存取最后结果集
    let result = new Array();
    //头指针
    let head;
    //尾指针
    let end;
    //排序
    nums.sort((a, b) => {
    	return a-b;
    });
    // 开始遍历
    for (let i = 0; i < nums.length; i++) {
        // 如果前后元素相同，跳过此次循环
        if(nums[i] === nums[i-1]) continue;
        //一开始的固定值为nums[0],所以头指针为 i+1 下一个元素
        head = i+1;
        //尾指针
        end = nums.length - 1;
        //如果头指针小于尾指针元素
        while(head < end){
            //判断固定值+头指针+尾指针是否等于0
            if(nums[head] + nums[end] + nums[i] === 0){
                //声明数组，存放这三个值
                let group =  new Array();
                group.push(nums[head]);
                group.push(nums[end]);
                group.push(nums[i]);
                result.push(group);
                //存放完毕之后，不要忘记头指针和尾指针的移动
                head += 1;
                end -= 1;
                //如果头指针满足小于尾指针且移动后的指针和移动前的指针元素相等，再往前移动
                while(head < end && nums[head] === nums[head - 1]){
                    head += 1;
                }
                 //如果头指针满足小于尾指针且移动后的指针和移动前的指针元素相等，再往后移动
                while(head < end && nums[end] === nums[end + 1]){
                    end -= 1;
                }
             //小于 0 需要移动头指针，因为尝试着让数据比原有数据大一点
            }else if(nums[head] + nums[end] + nums[i] < 0){
                head++;
            }else{
                //否则，尾指针向前移动，让数据小于元数据
                end--;
            }
        } 
    }
    return result;
}
//测试
let nums = [-1, 0, 1, 2, -1, -4];
threeSum(nums);
```

