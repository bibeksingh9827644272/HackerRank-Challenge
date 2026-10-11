# Minimum Window Substring

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

Given two strings `s` and `t` of lengths `m` and `n` respectively, return  *the  **minimum window***   ***substring**  **of  *`s`*  such that every character in  *`t`*  (** including duplicates**) is included in the window *. If there is no such substring, return* the empty string *`""`.

The testcases will be generated such that the answer is  **unique**.

 

 **Example 1:** 

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

```

 **Example 2:** 

```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.

```

 **Example 3:** 

```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

```

 

 **Constraints:** 

- m == s.length
- n == t.length
- 1 <= m, n <= 105
- s and t consist of uppercase and lowercase English letters.

 

 **Follow up:**  Could you find an algorithm that runs in `O(m + n)` time?

## Solution

**Language:** Python  
**Runtime:** 66 ms (beats 63.16%)  
**Memory:** 19.7 MB (beats 73.94%)  
**Submitted:** 2026-10-11T17:37:57.947Z  

```py

from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if len(t) > len(s):
            return ""

        need = Counter(t)
        required = len(t)
        left = 0
        min_len = float("inf")
        start = 0

        for right, char in enumerate(s):
            if need[char] > 0:
                required -= 1

            need[char] -= 1

            # All characters from t are included
            while required == 0:
                window_len = right - left + 1

                if window_len < min_len:
                    min_len = window_len
                    start = left

                # Remove the leftmost character
                left_char = s[left]
                need[left_char] += 1

                if need[left_char] > 0:
                    required += 1

                left += 1

        if min_len == float("inf"):
            return ""

        return s[start:start + min_len]

```

---

[View on LeetCode](https://leetcode.com/problems/minimum-window-substring/)