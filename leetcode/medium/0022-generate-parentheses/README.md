# Generate Parentheses

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given `n` pairs of parentheses, write a function to  *generate all combinations of well-formed parentheses*.

 

 **Example 1:** 

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]

```

 **Example 2:** 

```
Input: n = 1
Output: ["()"]

```

 

 **Constraints:** 

- 1 <= n <= 8

## Solution

**Language:** Python  
**Runtime:** 3 ms (beats 30.45%)  
**Memory:** 19.4 MB (beats 76.19%)  
**Submitted:** 2026-10-11T17:28:42.494Z  

```py

class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        result = []

        def backtrack(current, open_count, close_count):
            # If the string is complete, save it
            if len(current) == 2 * n:
                result.append(current)
                return

            # Add '(' if we have not used all open parentheses
            if open_count < n:
                backtrack(current + "(", open_count + 1, close_count)

            # Add ')' only if it won't make the string invalid
            if close_count < open_count:
                backtrack(current + ")", open_count, close_count + 1)

        backtrack("", 0, 0)
        return result

```

---

[View on LeetCode](https://leetcode.com/problems/generate-parentheses/)