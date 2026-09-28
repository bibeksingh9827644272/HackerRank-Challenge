# Add Binary

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

Given two binary strings `a` and `b`, return  *their sum as a binary string*.

 

 **Example 1:** 

```
Input: a = "11", b = "1"
Output: "100"

```

 **Example 2:** 

```
Input: a = "1010", b = "1011"
Output: "10101"

```

 

 **Constraints:** 

- 1 <= a.length, b.length <= 104
- a and b consist only of '0' or '1' characters.
- Each string does not contain leading zeros except for the zero itself.

## Solution

**Language:** Python  
**Runtime:** 3 ms (beats 41.17%)  
**Memory:** 19.3 MB (beats 52.79%)  
**Submitted:** 2026-09-28T18:07:33.678Z  

```py
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        i = len(a) - 1
        j = len(b) - 1
        carry = 0
        result = []

        while i >= 0 or j >= 0 or carry:
            total = carry

            if i >= 0:
                total += ord(a[i]) - ord('0')
                i -= 1

            if j >= 0:
                total += ord(b[j]) - ord('0')
                j -= 1

            result.append(str(total % 2))
            carry = total // 2

        return ''.join(reversed(result))
```

---

[View on LeetCode](https://leetcode.com/problems/add-binary/)