# Pascal's Triangle II

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

Given an integer `rowIndex`, return the `rowIndexth` (**0-indexed**) row of the  **Pascal's triangle**.

In  **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

 

 **Example 1:** 

```
Input: rowIndex = 3
Output: [1,3,3,1]

```

 **Example 2:** 

```
Input: rowIndex = 0
Output: [1]

```

 **Example 3:** 

```
Input: rowIndex = 1
Output: [1,1]

```

 

 **Constraints:** 

- 0 <= rowIndex <= 33

 

 **Follow up:**  Could you optimize your algorithm to use only `O(rowIndex)` extra space?

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.1 MB (beats 98.73%)  
**Submitted:** 2026-10-03T05:21:38.735Z  

```py
class Solution:
    def getRow(self, rowIndex: int):
        row = [1]

        for i in range(rowIndex):
            for j in range(i, 0, -1):
                row[j] = row[j] + row[j - 1]
            row.append(1)

        return row
```

---

[View on LeetCode](https://leetcode.com/problems/pascals-triangle-ii/)