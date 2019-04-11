---
Time：2019/4/11
Title: Valid Parentheses
Difficulty: Easy
Author: 小鹿
---



## 题目：Valid Parentheses

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```



## Solve: 

#### ▉ 算法思路

> 1、首先，我们通过上边的例子可以分析出什么样子括号匹配是复合物条件的，两种情况。
>
> - 第一种（非嵌套情况）：`{} []` ；
> - 第二种（嵌套情况）：`{ [ ( ) ] }` 。
>
> 除去这两种情况都不是符合条件的。
>
> 2、然后，我们将这些括号自右向左看做栈结构，右侧是栈顶，左侧是栈尾。
>
> 3、如果编译器中的括号左括号，我们就入栈（左括号不用检查匹配）；如果是右括号，就取出栈顶元素检查是否匹配。（提前将成对的括号通过键值对的方式存到散列表中）
>
> 4、如果匹配，就出栈。否则，就返回 false；





#### ▉ 代码实现

> 下方代码在标准的 Leetcode 测试中并不是最省内存和效率高的，因为我们用到了 Map，在内

```javascript
var isValid = function(s) {
    let stack = [];
    //将括号匹配存入散列表中
    let map = new Map();
    map.set(")","(");
    map.set("]","[");
    map.set("}","{");
	// 取出字符串中的括号
    for(let i = 0; i < s.length; i++){
        let c = s[i];
        //如果是右括号，如果栈中不为空就出栈栈顶数据
        if(map.has(c)){
            //判断栈此时是否为0
            if(stack.length !== 0){
                //如果栈顶元素不相同，就返回 false
                if(stack.pop() !== map.get(c)){
                    return false;
                }
            //如果此时栈内无元素，返回false
            }else{
                return false;
            }
        }else{
            //如果是左括号，就进栈
        	stack.push(c);
        }
    }
    //如果栈为空，括号全部匹配成功
    return stack.length === 0;
};
let str = "({(})";
console.log(isValid(str));
```



#### ▉ 代码改进

> 1）该改进用对象替代了 Map，节省了内存空间。
>
> 2）在判断时，没有用到提前存储的结构，直接使用当遇到左括号是直接入栈，提高了执行效率。

```
var isValid = function(s) {
    let stack = [];
    var obj = {
        "]": "[",
        "}": "{",
        ")": "(",
    };

    for(var i = 0; i < s.length; i++) {
        if(s[i] === "[" || s[i] === "{" || s[i] === "(") {
            stack.push(s[i]);
        } else {
            var key = stack.pop();
            if(maps[key] !== s[i]) {
                return false;
            }
        }
    }
    if(!stack.length) {
        return true;
    }
    return false;
};
```



#### ▉ 复杂度分析

> **时间复杂度： **O（n）。只需要遍历一遍字符串中的字符，入栈和出栈的时间复杂度为 O(1)。
>
> **空间复杂度：** O（n）。当只有左括号近栈，没有右括号进行匹配的时候是最糟糕的情况，所有括号都在栈内。例如：{{{{{{{{{





















