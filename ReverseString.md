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

> 1）反转字符串，第一想到的就是将字符窗倒序存储到数组中，可以先输出，然后再 for 循环加入到数组中。题目中要求需要原地修改输入数组，那么我们再想一个办法。
>
> 2）数组中的操作，需要原地修改数组，第一想到的就是用到指针，为什么能想到用指针呢？当你做这种数组的也好还是链表的也好，做多了之后，下意识的给出解决方法然后去看看可不可行。



###### ▉ 算法思路

> 通过以上分析，得出两种方法：
>
> - 字符串反转法
> - 双指针法
>
> 字符串反转法：
>
> 1）字符串反转法很简单了，按照我们正常的思路走就可以了，首先输出数组中的字符拼接成字符串。
>
> 2）然后从字符串尾部开始遍历，正向输入数组。
>
> 双指针法：
>
> 1）定义两个指针，分别指向字符串头部和尾部。
>
> 2）两个指针指向的值进行交换。
>
> 3）注意终止条件。
>
> - 如果为偶数，当头指针 - 1 等于尾指针时，反转完毕。
> - 如果为奇数，当两个指针相等时，反转完毕。



###### ▉ 测试用例

> 1）空字符串。
>
> 2）偶数个数的字符串。
>
> 3）奇数个数的字符串。
>
> 4）长度为 1 的字符串。



###### ▉ 双指针法

```javascript
var reverseString = function(s) {
    //判断输入的字符串是否为空
   if(s.length ==0) return s;
	//定义两个指针
    let low = 0;
    let high = s.length - 1;
	// 循环反转字符
    while(true){
        // 分为奇数/偶数两种可能
        if(low === high || high + 1 === low) break;
        let temp = s[low];
        s[low] = s[high];
        s[high] = temp;
        low++;
        high--;
    }
    // 返回反转好的字符串
    return s;
};
```



###### ▉ 字符串反转法

```javascript
var reverseString = function(s) {
    //判断输入的字符串是否为空
    if(s.length ==0) return s;
    let str = "";
    // 输出字符串
    for(let i in s){
        str = str+`${s[i]}`;
    }
    // 反转字符串输入
    for(let i = s.length - 1,j = 0;i >= 0;i--,j++){
        s[j] = str.charAt(i);
    }
    //返回反转好的字符串
    return s;
};
```



###### ▉ 性能分析

> 字符串反转法
>
> - 时间复杂度：O（n）。遍历整个数组，时间复杂度为 O（n）。
> - 空间复杂度：O（n）。输出数组需要额外的存储空间，如果用数组存储，需要开辟大小为 n 大小的内存空间。如果需要数组输出拼接字符串，空间复杂度为 O(1) 了。
>
> 双指针法：
>
> - 时间复杂度：O（n）。需要遍历 n/2 的数据，时间复杂度为 O(n)。
> - 空间复杂度：O（n）。只需常量级别的内存空间，空间复杂度为O（1）。



###### ▉ 考查内容

> 1）对字符串的基本操作。
>
> 2）数组的基本操作。

