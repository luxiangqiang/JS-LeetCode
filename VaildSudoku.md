---
Time：2019/4/29
Title: Valid Sudoku
Difficulty: Medium
Author: 小鹿
---



## 题目：Valid Sudoku (有效的数独)

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png) 

A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

**Example 1:**

```
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```

**Example 2:**

```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
- The given board contain only digits `1-9` and the character `'.'`.
- The given board size is always `9x9`.



## Solve:

###### ▉ 问题分析



###### ▉ 算法思路



###### ▉ 代码实现

```javascript
var isValidSudoku = function(board) {
    let mapRow = new Set();
    let mapColumn = new Set();
    let mapBorder = new Set();
    for(let i = 0;i < 9;i++){
        for(let j = 0;j < 9;j++){
            // 判断当前每行
            if(board[i][j] !== '.'){
                if(mapRow.has(board[i][j])){
                    return false;
                }else{
                    mapRow.add(board[i][j])
                }
            }
            // 判断当前每列
            if(board[j][i] !== '.'){
                if(mapColumn.has(board[j][i])){
                    return false;
                }else{
                    mapColumn.add(board[j][i])
                }
            }
        }
        mapRow.clear();
        mapColumn.clear();
    }
    // 判断当前 3x3 格子
    let arr = [0,3,6]
    for(let i = 0;i < 3;i ++ ){
        for(let j = 0;j < 3;j ++ ){
            for(let x1 = arr[i];x1 < arr[i] + 3;x1++){
                for(let y1 = arr[j];y1 < arr[j] + 3;y1++){
                    if(board[x1][y1] !== '.'){
                        if(mapBorder.has(board[x1][y1])){
                            return false;
                        }else{
                            mapBorder.add(board[x1][y1])
                        }
                    }
                }
            }
            mapBorder.clear();
        }
    }
    return true;
};
```















