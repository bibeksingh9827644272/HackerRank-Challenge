# Minimum Path Sum

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

 **Note:**  You can only move either down or right at any point in time.

 

 **Example 1:** 

```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.

```

 **Example 2:** 

```
Input: grid = [[1,2,3],[4,5,6]]
Output: 12

```

 

 **Constraints:** 

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 200
- 0 <= grid[i][j] <= 200

## Solution

**Language:** Python  
**Runtime:** 11 ms (beats 54.73%)  
**Memory:** 21.1 MB (beats 84.05%)  
**Submitted:** 2026-10-21T17:21:09.408Z  

```py
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])

        for i in range(m):
            for j in range(n):
                if i == 0 and j == 0:
                    continue
                elif i == 0:
                    grid[i][j] += grid[i][j - 1]
                elif j == 0:
                    grid[i][j] += grid[i - 1][j]
                else:
                    grid[i][j] += min(grid[i - 1][j], grid[i][j - 1])

        return grid[m - 1][n - 1]
```

---

[View on LeetCode](https://leetcode.com/problems/minimum-path-sum/)