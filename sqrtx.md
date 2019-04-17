---
Time：2019/4/17
Title: sqrt(x)
Difficulty: Easy
Author: 小鹿
---





## 题目：sqrt(x)

Implement `int sqrt(int x)`.

Compute and return the square root of *x*, where *x* is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

> 实现 `int sqrt(int x)` 函数。
>
> 计算并返回 *x* 的平方根，其中 *x* 是非负整数。
>
> 由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

**Example 1:**

```
Input: 4
Output: 2
```

**Example 2:**

```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```



## Solve:

###### ▉ 问题分析





###### ▉ 算法思路





###### ▉ 代码实现

```javascript
var mySqrt = function(x) {
    let low = 1;
    let high = x;
    if(x < 0) return -1;
    while(low <= high){
        let mid = Math.floor((low + high)/2);
        if(Math.pow(mid,2) <= x){
            if(Math.pow(mid+1,2) > x || mid === high){
                return mid;
            }else{
                low = mid + 1;
            }
        }else{
            high = mid - 1;
        }
    }
    return 0;
};
```









