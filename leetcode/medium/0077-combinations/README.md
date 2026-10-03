# Combinations

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given two integers `n` and `k`, return  *all possible combinations of*  `k`  *numbers chosen from the range*  `[1, n]`.

You may return the answer in  **any order**.

 

 **Example 1:** 

```
Input: n = 4, k = 2
Output: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Explanation: There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.

```

 **Example 2:** 

```
Input: n = 1, k = 1
Output: [[1]]
Explanation: There is 1 choose 1 = 1 total combination.

```

 

 **Constraints:** 

- 1 <= n <= 20
- 1 <= k <= n

## Solution

**Language:** Python  
**Runtime:** 109 ms (beats 50.90%)  
**Memory:** 61.1 MB (beats 96.36%)  
**Submitted:** 2026-10-03T05:18:40.231Z  

```py
class Solution:
    def combine(self, n: int, k: int):
        result = []
        current = []

        def backtrack(start):
            # If we selected k numbers, save the combination
            if len(current) == k:
                result.append(current.copy())
                return

            # Try every possible next number
            for num in range(start, n + 1):
                current.append(num)

                # Continue with numbers after num
                backtrack(num + 1)

                # Remove the last number (backtrack)
                current.pop()

        backtrack(1)
        return result
```

---

[View on LeetCode](https://leetcode.com/problems/combinations/)