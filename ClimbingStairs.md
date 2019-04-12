---
Time：2019/4/12
Title:Clibing Srairs
Difficulty: Easy
Author:小鹿
---



## 题目：Climbing Stairs

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given *n* will be a positive integer.

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

**Example 1:**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```



## slove

#### ▉ 算法思路

> 二种解决思路，第一利用递归；第二利用动态规划。
>
> 1）递归的实现方式：
>
> 首先，我们要知道递归使用应该满足的三个条件，之前在前边的题型中讲到过，后边我会整理成系列文章供大家方便学习。然后按照我们之前讲过的方式去写出递归公式，然后转化为递归的代码。我们会发现递归的时间复杂度为 O（2^n），我们是否还记得递归的缺点有一条就是警惕递归重复元素计算。就是因为有了重复元素的计算，导致了时间复杂度成指数的增长。
>
> 为了能够降低时间复杂度，我们可以用散列表来记录重复元素记录过的值，但是需要申请额外的空间进行存储，导致空间复杂度为O(n)，时间复杂度降为O(n)，也正是利用了空间换时间的思想。
>
> 2）动态规划的实现方式：
>
> 我们可以仔细发现上方的递归的方式还是可以优化的，我们换种方式去思考，从底向上去思考，其实我们计算一个值之存储之前的两个值就可以了（比如：计算 f(6) ,需要知道 f(5) 和 f(4) 的值就可以了），我们可以不用存储之前的值，此时可以将空间复杂度降为 O(1)。



#### ▉ 代码实现（递归）

> 优化后的递归实现。

```javascript
//递归实现
//时间复杂度为 O(n)，空间复杂度为 O(n)
var climbStairs = function(n) {
    let map = new Map();
    if(n === 1) return 1;
    if(n === 2) return 2;
    if(map.has(n)){
    	return map.get(n);
    }else{
        let value = climbStairs(n - 1) +climbStairs(n - 2);
        map.set(n,value);
        return value;
    }
};
```



#### ▉ 代码实现（动态规划）

```javascript
//动态规划
//时间复杂度为O(n) 空间复杂度为O(1)
var climbStairs = function(n) {
    if(n < 1) return 0;
    if(n === 1) return 1;
    if(n === 2) return 2;

    let a = 1;
    let b = 2;
    let temp = 0;

    for (let i = 3; i < n + 1; i++) {
        temp = a + b;
        a = b;
        b = temp;          
    }
    return temp;
}
```





















