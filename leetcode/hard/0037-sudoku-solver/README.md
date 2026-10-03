# Sudoku Solver

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy  **all of the following rules** :

- Each of the digits 1-9 must occur exactly once in each row.
- Each of the digits 1-9 must occur exactly once in each column.
- Each of the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.

The `'.'` character indicates empty cells.

 

 **Example 1:** 

```
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution is shown below:

```

 

 **Constraints:** 

- board.length == 9
- board[i].length == 9
- board[i][j] is a digit or '.'.
- It is guaranteed that the input board has only one solution.

## Solution

**Language:** Python  
**Runtime:** 2 ms  
**Memory:** 19.3 MB  
**Submitted:** 2026-10-03T13:55:33.654Z  

```py
class Solution:
    def solveSudoku(self, board):
        def isValid(row, col, num):
            # Check row
            for j in range(9):
                if board[row][j] == num:
                    return False

            # Check column
            for i in range(9):
                if board[i][col] == num:
                    return False

            # Check 3x3 box
            start_row = (row // 3) * 3
            start_col = (col // 3) * 3

            for i in range(start_row, start_row + 3):
                for j in range(start_col, start_col + 3):
                    if board[i][j] == num:
                        return False

            return True

        def backtrack():
            best_row = -1
            best_col = -1
            best_nums = None

            # Find the empty cell with the fewest choices
            for row in range(9):
                for col in range(9):
                    if board[row][col] == ".":
                        possible = []

                        for num in "123456789":
                            if isValid(row, col, num):
                                possible.append(num)

                        # No number can be placed here
                        if len(possible) == 0:
                            return False

                        # Choose the cell with minimum choices
                        if best_nums is None or len(possible) < len(best_nums):
                            best_nums = possible
                            best_row = row
                            best_col = col

                            # Only one choice - best possible case
                            if len(best_nums) == 1:
                                break

                if best_nums is not None and len(best_nums) == 1:
                    break

            # No empty cells -> Sudoku solved
            if best_nums is None:
                return True

            # Try possible numbers
            for num in best_nums:
                board[best_row][best_col] = num

                if backtrack():
                    return True

                # Undo
                board[best_row][best_col] = "."

            return False

        backtrack()
```

---

[View on LeetCode](https://leetcode.com/problems/sudoku-solver/)