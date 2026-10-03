# Permutations

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in  **any order**.

 

 **Example 1:** 

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

```

 **Example 2:** 

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]

```

 **Example 3:** 

```
Input: nums = [1]
Output: [[1]]

```

 

 **Constraints:** 

- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- All the integers of nums are unique.

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.7 MB (beats 10.54%)  
**Submitted:** 2026-10-03T14:01:39.420Z  

```py
class Solution:
    def permute(self, nums):
        result = []

        def backtrack(current):
            # A complete permutation
            if len(current) == len(nums):
                result.append(current.copy())
                return

            for num in nums:
                # Don't use the same number twice
                if num in current:
                    continue

                current.append(num)

                # Continue building the permutation
                backtrack(current)

                # Undo the choice
                current.pop()

        backtrack([])
        return result
```

---

[View on LeetCode](https://leetcode.com/problems/permutations/)