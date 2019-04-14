---
Time：2019/4/14
Title: Evaluate Reverse Polish Notation
Difficulty: Medium
Author:小鹿
---



## 题目：Evaluate Reverse Polish Notation

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, `/`. Each operand may be an integer or another expression.

**Note:**

- Division between two integers should truncate toward zero.
- The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.

> 根据[逆波兰表示法](https://baike.baidu.com/item/%E9%80%86%E6%B3%A2%E5%85%B0%E5%BC%8F/128437)，求表达式的值。
>
> 有效的运算符包括 `+`, `-`, `*`, `/` 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。
>
> **说明：**
>
> - 整数除法只保留整数部分。
> - 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

**Example 1:**

```
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**

```
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**

```
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```



## Solve:

###### ▉ 算法思路



###### ▉ 代码实现

```javascript
var evalRPN = function(tokens) {
   // 声明栈
    let stack = [];
    for(let item of tokens){
        switch(item){
            case '+':
                let a1 = stack.pop();
                let b1 = stack.pop();
                stack.push(b1 + a1);
                break;
            case '-':
                let a2 = stack.pop();
                let b2 = stack.pop();
                stack.push(b2 - a2);
                break;
            case '*':
                let a3 = stack.pop();
                let b3 = stack.pop();
                stack.push(b3 * a3);
                break;
            case '/':
                let a4 = stack.pop();
                let b4 = stack.pop();
                stack.push(parseInt(b4 / a4));
                break;
            default: 
                stack.push(parseInt(item));
        }
    }
    return parseInt(stack.pop());
};
```





















