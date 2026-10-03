# Permutations II

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a collection of numbers, `nums`, that might contain duplicates, return  *all possible unique permutations  **in any order**.* 

 

 **Example 1:** 

```
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]

```

 **Example 2:** 

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

```

 

 **Constraints:** 

- 1 <= nums.length <= 8
- -10 <= nums[i] <= 10

## Solution

**Language:** Python  
**Runtime:** 3 ms (beats 89.98%)  
**Memory:** 19.8 MB (beats 76.38%)  
**Submitted:** 2026-10-03T14:02:20.633Z  

```py
class Solution:
    def permuteUnique(self, nums):
        nums.sort()
        result = []
        used = [False] * len(nums)

        def backtrack(current):
            if len(current) == len(nums):
                result.append(current.copy())
                return

            for i in range(len(nums)):
                if used[i]:
                    continue

                # Skip duplicates
                if i > 0 and nums[i] == nums[i - 1] and not used[i - 1]:
                    continue

                used[i] = True
                current.append(nums[i])

                backtrack(current)

                current.pop()
                used[i] = False

        backtrack([])
        return result
```

---

[View on LeetCode](https://leetcode.com/problems/permutations-ii/)