# Scramble String

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

We can scramble a string s to get a string t using the following algorithm:

- If the length of the string is 1, stop.
- If the length of the string is > 1, do the following: Split the string into two non-empty substrings at a random index, i.e., if the string is s, divide it to x and y where s = x + y. Randomly decide to swap the two substrings or to keep them in the same order. i.e., after this step, s may become s = x + y or s = y + x. Apply step 1 recursively on each of the two substrings x and y.

Given two strings `s1` and `s2` of  **the same length**, return `true` if `s2` is a scrambled string of `s1`, otherwise, return `false`.

 

 **Example 1:** 

```
Input: s1 = "great", s2 = "rgeat"
Output: true
Explanation: One possible scenario applied on s1 is:
"great" --> "gr/eat" // divide at random index.
"gr/eat" --> "gr/eat" // random decision is not to swap the two substrings and keep them in order.
"gr/eat" --> "g/r / e/at" // apply the same algorithm recursively on both substrings. divide at random index each of them.
"g/r / e/at" --> "r/g / e/at" // random decision was to swap the first substring and to keep the second substring in the same order.
"r/g / e/at" --> "r/g / e/ a/t" // again apply the algorithm recursively, divide "at" to "a/t".
"r/g / e/ a/t" --> "r/g / e/ a/t" // random decision is to keep both substrings in the same order.
The algorithm stops now, and the result string is "rgeat" which is s2.
As one possible scenario led s1 to be scrambled to s2, we return true.

```

 **Example 2:** 

```
Input: s1 = "abcde", s2 = "caebd"
Output: false

```

 **Example 3:** 

```
Input: s1 = "a", s2 = "a"
Output: true

```

 

 **Constraints:** 

- s1.length == s2.length
- 1 <= s1.length <= 30
- s1 and s2 consist of lowercase English letters.

## Solution

**Language:** Python  
**Runtime:** 27 ms (beats 28.23%)  
**Memory:** 21.3 MB (beats 25.18%)  
**Submitted:** 2026-10-11T17:38:53.331Z  

```py

from functools import lru_cache
from collections import Counter

class Solution:
    def isScramble(self, s1: str, s2: str) -> bool:
        if len(s1) != len(s2):
            return False

        @lru_cache(None)
        def solve(a: str, b: str) -> bool:
            if a == b:
                return True

            # Prune if character frequencies differ
            if Counter(a) != Counter(b):
                return False

            n = len(a)

            for i in range(1, n):
                # Case 1: No swap
                if solve(a[:i], b[:i]) and solve(a[i:], b[i:]):
                    return True

                # Case 2: Swap
                if solve(a[:i], b[n-i:]) and solve(a[i:], b[:n-i]):
                    return True

            return False

        return solve(s1, s2)

```

---

[View on LeetCode](https://leetcode.com/problems/scramble-string/)