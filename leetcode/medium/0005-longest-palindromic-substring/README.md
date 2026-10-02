# Longest Palindromic Substring

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a string `s`, return  *the longest*   *palindromic*   *substring*  in `s`.

 

 **Example 1:** 

```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.

```

 **Example 2:** 

```
Input: s = "cbbd"
Output: "bb"

```

 

 **Constraints:** 

- 1 <= s.length <= 1000
- s consist of only digits and English letters.

## Solution

**Language:** Python  
**Runtime:** 0 ms  
**Memory:** 19.2 MB  
**Submitted:** 2026-10-02T10:04:14.683Z  

```py
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)

        if n <= 1:
            return s

        start = 0
        max_len = 1

        def expand(left, right):
            while left >= 0 and right < n and s[left] == s[right]:
                left -= 1
                right += 1

            return left + 1, right - 1

        for i in range(n):
            # Odd-length palindrome
            left, right = expand(i, i)

            if right - left + 1 > max_len:
                start = left
                max_len = right - left + 1

            # Even-length palindrome
            left, right = expand(i, i + 1)

            if right - left + 1 > max_len:
                start = left
                max_len = right - left + 1

        return s[start:start + max_len]
```

---

[View on LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)