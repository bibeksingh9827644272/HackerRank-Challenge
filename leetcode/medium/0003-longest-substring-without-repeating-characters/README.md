# Longest Substring Without Repeating Characters

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a string `s`, find the length of the  **longest**   **substring**  without duplicate characters.

 

 **Example 1:** 

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3. Note that "bca" and "cab" are also correct answers.

```

 **Example 2:** 

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

```

 **Example 3:** 

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

```

 

 **Constraints:** 

- 0 <= s.length <= 105
- s consists of English letters, digits, symbols and spaces.

## Solution

**Language:** Python  
**Runtime:** 210 ms (beats 56.13%)  
**Memory:** 20 MB (beats 37.03%)  
**Submitted:** 2026-10-02T10:01:03.838Z  

```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        char_set = set()
        left = 0
        max_length = 0

        for right in range(len(s)):
            # Remove characters until there is no duplicate
            while s[right] in char_set:
                char_set.remove(s[left])
                left += 1

            # Add current character
            char_set.add(s[right])

            # Calculate current window length
            current_length = right - left + 1
            max_length = max(max_length, current_length)

        return max_length
```

---

[View on LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)