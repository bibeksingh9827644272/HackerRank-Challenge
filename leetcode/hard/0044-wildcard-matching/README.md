# Wildcard Matching

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

Given an input string (`s`) and a pattern (`p`), implement wildcard pattern matching with support for `'?'` and `'*'` where:

- '?' Matches any single character.
- '*' Matches any sequence of characters (including the empty sequence).

The matching should cover the  **entire**  input string (not partial).

 

 **Example 1:** 

```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".

```

 **Example 2:** 

```
Input: s = "aa", p = "*"
Output: true
Explanation: '*' matches any sequence.

```

 **Example 3:** 

```
Input: s = "cb", p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.

```

 

 **Constraints:** 

- 0 <= s.length, p.length <= 2000
- s contains only lowercase English letters.
- p contains only lowercase English letters, '?' or '*'.

## Solution

**Language:** Python  
**Runtime:** 3 ms (beats 94.98%)  
**Memory:** 19.3 MB (beats 67.42%)  
**Submitted:** 2026-10-11T17:32:59.629Z  

```py

class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        i = j = 0
        star = -1
        match = 0

        while i < len(s):
            # Exact match or '?' matches one character
            if j < len(p) and (p[j] == s[i] or p[j] == '?'):
                i += 1
                j += 1

            # Remember the position of '*'
            elif j < len(p) and p[j] == '*':
                star = j
                match = i
                j += 1

            # Try matching one more character with the last '*'
            elif star != -1:
                j = star + 1
                match += 1
                i = match

            # No match is possible
            else:
                return False

        # Skip any remaining '*' characters
        while j < len(p) and p[j] == '*':
            j += 1

        return j == len(p)

```

---

[View on LeetCode](https://leetcode.com/problems/wildcard-matching/)