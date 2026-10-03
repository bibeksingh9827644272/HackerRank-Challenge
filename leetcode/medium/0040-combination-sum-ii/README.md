# Combination Sum II

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used  **once**  in the combination.

 **Note:**  The solution set must not contain duplicate combinations.

 

 **Example 1:** 

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

```

 **Example 2:** 

```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]

```

 

 **Constraints:** 

- 1 <= candidates.length <= 100
- 1 <= candidates[i] <= 50
- 1 <= target <= 30

## Solution

**Language:** Python  
**Runtime:** 2 ms (beats 87.11%)  
**Memory:** 19.6 MB (beats 45.15%)  
**Submitted:** 2026-10-03T13:58:22.859Z  

```py
class Solution:
    def combinationSum2(self, candidates, target):
        candidates.sort()
        result = []

        def backtrack(start, remaining, current):
            if remaining == 0:
                result.append(current.copy())
                return

            for i in range(start, len(candidates)):
                # Skip duplicate values at the same level
                if i > start and candidates[i] == candidates[i - 1]:
                    continue

                # Since array is sorted
                if candidates[i] > remaining:
                    break

                current.append(candidates[i])

                # i + 1 because each number can be used only once
                backtrack(i + 1, remaining - candidates[i], current)

                # Undo choice
                current.pop()

        backtrack(0, target, [])
        return result
```

---

[View on LeetCode](https://leetcode.com/problems/combination-sum-ii/)