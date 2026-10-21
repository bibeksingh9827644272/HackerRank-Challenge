# Spiral Matrix II

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

 

 **Example 1:** 

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]

```

 **Example 2:** 

```
Input: n = 1
Output: [[1]]

```

 

 **Constraints:** 

- 1 <= n <= 20

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.3 MB (beats 78.47%)  
**Submitted:** 2026-10-21T16:38:26.639Z  

```py
class Solution:
    def generateMatrix(self, n: int) -> list[list[int]]:
        matrix = [[0] * n for _ in range(n)]

        num = 1
        top, bottom = 0, n - 1
        left, right = 0, n - 1

        while num <= n * n:
            for j in range(left, right + 1):
                matrix[top][j] = num
                num += 1
            top += 1

            for i in range(top, bottom + 1):
                matrix[i][right] = num
                num += 1
            right -= 1

            for j in range(right, left - 1, -1):
                if num <= n * n:
                    matrix[bottom][j] = num
                    num += 1
            bottom -= 1

            for i in range(bottom, top - 1, -1):
                if num <= n * n:
                    matrix[i][left] = num
                    num += 1
            left += 1

        return matrix
```

---

[View on LeetCode](https://leetcode.com/problems/spiral-matrix-ii/)