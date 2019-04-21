---
Time：2019/4/20
Title: Reverse Words In a String
Difficulty: Midumn
Author: 小鹿
---



## 题目：Reverse Words In a String（翻转字符串里的单词）

Given an input string, reverse the string word by word.

>  给定一个字符串，逐个翻转字符串中的每个单词。 

**Example 1:**

```
Input: "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: "  hello world!  "
Output: "world! hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

 

**Note:**

- A word is defined as a sequence of non-space characters.
- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
- You need to reduce multiple spaces between two words to a single space in the reversed string.

> **说明：**
>
> - 无空格字符构成一个单词。
> - 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
> - 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。



## Solve:

###### ▉ 问题分析

> 



###### ▉ 算法思路

> 



###### ▉ 测试用例

> 



###### ▉ 代码实现

```javascript
 var reverseWords = function(s) {
     // 判断当前的单词是否为空字符串
     if(s.length === 0) return "";

     let [index,len] = [0,s.length];
     let word = "";
     let result = "";

     while(index < len){
         // 跳过空格
         while(index < len && s.charAt(index) == ' '){
             index ++;
         }

         // 反转单词
         while(index < len && s.charAt(index) !== ' '){
             word = `${word}${s.charAt(index)}`;
             index ++;
         }
         // 拼接
         result = word + ' ' + result;
         word = "";
     }
     return result.trim(); 
 };
```



















