---
Time：2019/4/13
Title: Longest Vaild Parentheses
Difficulty: Difficulty
Author: 小鹿
---



## 题目：Longest Vaild Parentheses

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

```javascript
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

**Example 2:**

```javascript
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
```



## Solve:

###### ▉ 算法思路

> 通过栈来记录括号的有效长度。



###### ▉ 代码实现

```javascript
var longestValidParentheses = function(s) {
    // 存储最大有效长度
    let longest = 0;
    // 栈用来存储接下来遇到的匹配括号的长度
    let stk = [0];
    for (let i = 0; i < s.length; ++i) {
        // 如果为左括号，就入栈数字 0
        if (s[i] === '(') {
            stk.push(0);
        } else {
            // 如果为右括号，栈长度小于等于1，入栈 0 （占位）
            if (stk.length > 1) {
                // 取出当前刚入栈的长度数字
                let v = stk.pop();
                // 取出之前连续记录的有效长度
                let lastCount = stk[stk.length - 1];
                //将三者进行叠加（例：（（））情况）
                stk[stk.length - 1] = lastCount + v + 2;
                // longest 一直保存最长有效长度
                longest = Math.max(longest, stk[stk.length - 1]);
            } else {
                //入栈 0 （占位）
                stk = [0];
            }
        }
    }
    return longest;
};
```































