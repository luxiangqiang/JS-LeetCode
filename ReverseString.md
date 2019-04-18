---
Time：2019/4/18
Title: Reverse String
Difficulty: Easy
Author: 小鹿
---



## 题目：Reverse String(反转字符串)

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

>  编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `char[]` 的形式给出。
>
> 不要给另外的数组分配额外的空间，你必须**原地修改输入数组**、使用 O(1) 的额外空间解决这一问题。
>
> 你可以假设数组中的所有字符都是 [ASCII](https://baike.baidu.com/item/ASCII) 码表中的可打印字符。

**Example 1:**

```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```



## Slove:

###### ▉ 问题分析

> 



###### ▉ 算法思路

> 



###### ▉ 测试用例

> 



###### ▉ 双指针法

```javascript
var reverseString = function(s) {
   if(s.length ==0) return s;

    let low = 0;
    let high = s.length - 1;

    while(true){
        if(low === high || high + 1 === low) break;
        let temp = s[low];
        s[low] = s[high];
        s[high] = temp;
        low++;
        high--;
    }
    return s;
};
```



###### ▉ 性能分析

> 



###### ▉ 考查内容

> 

