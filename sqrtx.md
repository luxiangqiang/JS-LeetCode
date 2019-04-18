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
> 计算并返回 *x* 的平方根，其中 *x* 是非负整数。「」
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

> 1）根据题目要求，求一个指定树的平方根，第一要想到的是开平方根是没有规律可循的，可能想到一个暴力破解法，从 1 开始遍历，直到满足 `k^2 < x `且 `(k+1)^2 > x` 为止。
>
> 2) 你可能想到这种方法效率太低，需要从 1 开始，如果 x 很大，岂不是需要遍历很多？能不能规定一个范围，在这个范围中查找开平方根呢？你会想到，所有数的开平方根得到的值是永远小于等于自身的（0 是自身），所以 x 的开平方根的值的范围一定在 0 < k < x 之间。
>
> 3）要想在这个区间快速定位找到一个满足条件的 x ，最高效的方法莫过于二分查找，但是可能存在小数，这又涉及到二分查找的四个变体（二分查找的变形）过程。如果你之前没有连接过，没关系，请看我之前记载的一篇文章。
>
> 4）虽然我们已经确定了解题方法，但是这时候不要着急，想一想这个问题是否满足二分查找的四个适用条件？哪四个条件呢？你需要系统学习一下就 ok ！



###### ▉ 算法思路

> 1）此过程分为两种情况，负数和正整数，所以要对输入的 x 进行判断。
>
> 2）然后开始根据二分查找应该注意的「三个重点」写出无 bug 的代码。
>
> 3）对二分查找进行稍微的变体，因为我们可能查找的数并不是一个正整数，我们取整数部分就可以了，小数部分省略。



###### ▉ 测试用例

> 1）输入 0 
>
> 2）输入1
>
> 3）输入负数的 x
>
> 4）输入平方根为正整数的 x
>
> 5）输入平方根为小数的 x



###### ▉ 代码实现

> 写二分查找代码需要注意的三点：
>
> 1）循环退出条件。
>
> 2）mid 的取值。
>
> 3）low 和 hight 的更新。

```javascript
var mySqrt = function(x) {
     let low = 1;
     let high = x;
     // 如果 x 小于 0 输出 -1
     if(x < 0) return -1;
     // 循环终止条件
     while(low <= high){
        // mid 取值
        let mid = Math.floor(low + ((high - low)/2));
        // 判断平方是否小于等于
        if(Math.pow(mid,2) <= x){
            // 如果小于等于,如果下一值大于 x 则当前值为 x 平方根的最小整数值
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



###### ▉ 性能分析

> 暴力破解：
>
> - 时间复杂度：O（n）。你需要从 1 遍历所有可能的数据，所以时间复杂度为O（n）。
> - 空间复杂度：O（1）。不需要额外的内存空间。
>
> 二分法：
>
> - 时间复杂度：O（n）。每次都折半查找，所以查找一个元素时间复杂度为O（logn）。
> - 空间复杂度：O（1）。不需要额外的内存空间。



###### ▉ 小结

> 通过这个题我们可以总结一下：
>
> 1）如果问题涉及到查找，我们要想到使用二分查找来提高效率。
>
> 2）使用二分查找之前，判断问题是否满足二分查找的要求。

