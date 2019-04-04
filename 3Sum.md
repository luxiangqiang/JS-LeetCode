---
Time：2019/4/3
Title:3Sum
Difficulty: medium
Author:小鹿
---



#### 题目三：ADD Two Numbers

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero. 

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



**Solve:** 

###### ▉ 算法思路：

> 1、直接用三个 for 循环遍历所有数据，找出符合条件的数据，时间复杂度为 O(n^3)。能不能更快效率？
>
> 2、先对数组内数据进行一次排序。O(nlogn)
>
> 3、最外层一个 for 循环,先把其中一个值固定住(存放到变量)，然后分别用两个指针指向数据的非固定值的头部和尾部，通过 while 循环来遍历。
>
> 4、如果三个数据相加等于 0 了，就存储该三个值且更新 head 和 end 指针。
>
> 5、如果不等于小于或大于 0 ,就更新 head 和 end 指针移动重新查找符合条件的值。
>
> 6、返回结果集 result。



###### ▉ 边界条件：

> 1、判断数组内元素是否都为整数或负数，直接返回。
>
> 2、判断固定值、head 以及 end 指针的值前后元素是否相同，去掉重复计算。
>
> 3、判断 head 和 end 指针的大小关系。
>
> 4、注意去掉重复数据



###### ▉ 代码实现：

```javascript
  /**
  * @param {number[]} nums
  * @return {number[][]}
  */

var threeSum = function(nums) {
    //用来存取最后结果集
    let result = new Array();
    //头指针
    let head;
    //尾指针
    let end;
    //固定值
    let fixedVal;

    //排序
    nums.sort((a, b) => {
    	return a-b;
    });
    
    //判断数组内元素是否都为整数或负数，直接返回
    if(nums[0] > 0 || nums[nums.length - 1] < 0) return result;
    
    // 开始遍历
    for (let i = 0; i < nums.length; i++) {
        //固定值
		fixedVal = nums[i];
        // 如果前后元素相同，跳过此次循环（固定值）
        if(fixedVal === nums[i-1]) continue;
        //一开始的固定值为nums[0],所以头指针为 i+1 下一个元素
        head = i+1;
        //尾指针
        end = nums.length - 1;
        //如果头指针小于尾指针元素
        while(head < end){
            //判断固定值+头指针+尾指针是否等于0
            if(nums[head] + nums[end] + fixedVal === 0){
                //声明数组，存放这三个值
                let group =  new Array();
                group.push(nums[head]);
                group.push(nums[end]);
                group.push(fixedVal);
                result.push(group);
                //存放完毕之后，不要忘记头指针和尾指针的移动(否则会产生死循环)
                head += 1;
                end -= 1;
                //如果头指针满足小于尾指针且移动后的指针和移动前的指针元素相等，再往前移动
                while(head < end && nums[head] === nums[head - 1]){
                    head += 1;
                }
                 //如果头指针满足小于尾指针且移动后的指针和移动前的指针元素相等，再往后移动
                while(head < end && nums[end] === nums[end + 1]){
                    end -= 1;
                }
             //小于 0 需要移动头指针，因为尝试着让数据比原有数据大一点
            }else if(nums[head] + nums[end] + fixedVal < 0){
                head++;
            }else{
                //否则，尾指针向前移动，让数据小于元数据
                end--;
            }
        } 
    }
    return result;
}
//测试
let nums = [-1, 0, 1, 2, -1, -4];
let result = threeSum(nums);
for(let item in result){
    console.log(result[item])
}
```



###### ▉ sort 排序：

> **定义**：sort() 方法用于对数组的元素进行排序。 在原来数组上进行排序，不生成副本。
>
> **使用：**
>
> 1）无参：按照字母的顺序对元素排序，即便是数字，先转换 String 再排序（按照字符编码），往往得不到我们要的结果。
>
> 2）有参：参数为比较函数，比较函数有两个参数 a,b （默认的 a 是小于 b 的）
>
> - 若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。（从小到大）
> - 若 a 等于 b，则返回 0。（按照无参排序）
> - 若 a 大于 b，则返回一个大于 0 的值。（从大到小）
>
> **内部实现：**
>
> 在 Chrome 浏览器中 sort 的你内部实现是快速排序，但是 FireFox 内部使用的归并排序，两者的区别就是快速排序不如归并排序稳定，但是大多数情况下还是可以使用快排的，只有个别要求必须稳定。所谓的稳定性就是原始数据相同的元素在排序之后位置是否改变？
>
> **性能问题：**
>
> 1、sort 会产生性能问题，因为无论是快排还是归并，都涉及到递归，如果递归深度过大，导致堆栈溢出，v8 引擎的解决办法就是设置一个递归深度阈值，小于阀值采用插入排序，大于阀值改用快排。
>
> 2、快排在在最差的情况下算法也会退化，因为根据 pivot 选择的不同，最坏情况时间复杂度退化到 O(n^2).
>
> 3、怎么进行改进？有兴趣可以看下方参考链接！
>
> 参考链接：https://efe.baidu.com/blog/talk-about-sort-in-front-end/







