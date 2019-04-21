---
Time：2019/4/19
Title: String To Integer
Difficulty: Medium
Author: 小鹿
---



## 题目：String To Integer（字符串转换整数 (atoi)）

Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

> 请你来实现一个 `atoi` 函数，使其能将字符串转换成整数。
>
> 首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。
>
> 当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。
>
> 该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。
>
> 注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。
>
> 在任何情况下，若函数不能进行有效的转换时，请返回 0。
>
> **说明：**
>
> 假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−231,  231 − 1]。如果数值超过这个范围，qing返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

**Note:**

- Only the space character `' '` is considered as whitespace character.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

**Example 1:**

```
Input: "42"
Output: 42
```

**Example 2:**

```
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```

**Example 3:**

```
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```

**Example 4:**

```
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
```

**Example 5:**

```
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```



## Solve:

###### ▉ 问题分析

> 将字符串转化为数字，根据题目要求可以分出一下几种情况：
>
> - 如果字符串都是数字，直接进行转换。
> - 如果字符串中只有数字和空格，要跳过空格，只输出数字。
> - 数字前正负号要保留。
> - 如果字符串中有数字和字母。
>   - 字母在数字前，直接返回数字 0 ;
>   - 字母在数字后，忽略数字后的字母；
> - 如果输出的数字大于限制值，输出规定的限制值。
> - 如果输出的数字小于限制值，输出规定的限制值。
>
> 上述将所有条件弄明白之后，然后进行规划解决上述问题：



###### ▉ 算法思路

> 整体将字符串转化为每个字符来进行判断：
>
> 1）空格：如果当前的字符为空格，直接跳过，判断下一字符。
>
> 2）符号位：如果判断当前的字符为 “ + ” 或 “ - “，用 sign 存储 1 或 -1，最后乘最后得出的数字。
>
> 3）只取数字：判断当前是否满足条件（0<=  c <=9），不满足条件直接跳出循环。
>
> 4）虽然取到数字，判断数字是否超出最大值/最小值，我们用判断位数，最大值为 7 位，每遍历一个数组，我们就进行乘以 10 加 个位数。



###### ▉ 测试用例

> 1）只输入数字字符串
>
> 2）带空格、负数的字符串
>
> 3）带字母的字符串
>
> 4）空字符串
>
> 5）超出限制的字符串



###### ▉ 代码实现

```javascript
var myAtoi = function(str) {
    // 最大值与最小值
    let MAX_VALUE = Math.pow(2,31)-1;
    let MIN_VALUE = -Math.pow(2,31);
    // 判断字符窗是否为空
    if(str == null || str.length == 0) return 0;
	// 初始化
    // sign：记录正负号
    // base: 记录数字的位数
    let [index,base,sign,len] = [0,0,1,str.length];

    // 跳过空格
    while(index < len && str.charAt(index) == ' '){
        index++;
    }

    // 获取符号位
    if(index < len && (str.charAt(index) == "+") || str.charAt(index) == '-'){	   // 记录正负号
        sign = 1 - 2 * ((str.charAt(index++) == '-') ? 1 : 0);
    }

    // 只取数字,碰到非数字退出循环
    while(index < len && parseInt(str.charAt(index)) >= 0 && parseInt(str.charAt(index)) <= 9){
        // 溢出判断，MAX_VALUE 的个位为 7
        if(base > parseInt(MAX_VALUE/10) || (base == parseInt(MAX_VALUE/10) && parseInt(str.charAt(index)) > 7)){
            if(sign == 1){
                return MAX_VALUE;
            }else{
                return MIN_VALUE;
            }
        } 
        // 记录位数
        base = base * 10 + parseInt(str.charAt(index++));                
    }
    // 返回符号位 * 当前字符串中的数字
    return sign * base;
};
```



###### ▉ 考查内容

> 1）对字符串的基本操作。
>
> 2）代码的全面性、鲁棒性。























