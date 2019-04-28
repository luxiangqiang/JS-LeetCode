---
Time：2019/4/28
Title: Number of Islands
Difficulty: Medium
Author: 小鹿
---



## 题目：Number of Islands（岛屿的数量）

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

> 给定一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。 

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```



## Solve:

###### ▉ 问题分析



###### ▉ 算法思路



###### ▉ 代码实现

```javascript
var numIslands = function(grid) {
    // 判断图是否为空
    if(grid.length === 0) return 0;
    // 数量
    let count = 0;
    dfsSearch = (grid,i,j) =>{
        if(i < 0 || j < 0 || i >= grid.length || j >= grid[0].length) return;

        if(grid[i][j] === '1'){
            grid[i][j] = '0';
            dfsSearch(grid,i,j + 1);
            dfsSearch(grid,i,j - 1);
            dfsSearch(grid,i + 1,j);
            dfsSearch(grid,i - 1,j);
        }
    }
    for(let i = 0;i < grid.length;i++){
        for(let j = 0;j < grid[0].length;j++){
            if(grid[i][j] === '1'){
                dfsSearch(grid,i,j);
                count++;
            }                   
        }
    }
    return count;
};
```



