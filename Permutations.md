---
Time：2019/4/30
Title: Permutations
Difficulty: Medium
Author: 小鹿
---



## 题目：Permutations（全排列）

Given a collection of **distinct** integers, return all possible permutations.

> 给定一个**没有重复**数字的序列，返回其所有可能的全排列。 

**Example:**

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```





## Solve:

###### ▉ 算法思路



###### ▉ 代码实现

```javascript
var permute = function(nums) {
    const nl = nums.length;
    if(nl === 0) {return [];}
    if(nl === 1) {return [nums];}
    const result = [];
    for(let i = 0; i < nl; i ++) {
        const subArr = [];
        for(let j = 0; j < nl; j ++) {
            if(i !== j) {
                subArr.push(nums[j]);
            }
        }
        const subRes = permute(subArr);
        const sl = subRes.length;
        for(let j = 0; j < sl; j ++){
            result.push([nums[i]].concat(subRes[j]));
        }
    }
    return result;
};

// 测试
let arr = [1,2,3];
console.log(permute(arr))
```













