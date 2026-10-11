# Restore IP Addresses

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

A  **valid IP address**  consists of exactly four integers separated by single dots. Each integer is between `0` and `255` (**inclusive**) and cannot have leading zeros.

- For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses, but "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses.

Given a string `s` containing only digits, return  *all possible valid IP addresses that can be formed by inserting dots into* `s`. You are  **not**  allowed to reorder or remove any digits in `s`. You may return the valid IP addresses in  **any**  order.

 

 **Example 1:** 

```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]

```

 **Example 2:** 

```
Input: s = "0000"
Output: ["0.0.0.0"]

```

 **Example 3:** 

```
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]

```

 

 **Constraints:** 

- 1 <= s.length <= 20
- s consists of digits only.

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.4 MB (beats 65.61%)  
**Submitted:** 2026-10-11T17:40:46.687Z  

```py

class Solution:
    def restoreIpAddresses(self, s: str) -> list[str]:
        result = []

        def backtrack(start: int, parts: list[str]) -> None:
            # A valid IP must contain exactly 4 parts
            if len(parts) == 4:
                if start == len(s):
                    result.append(".".join(parts))
                return

            # Try segments of length 1, 2, or 3
            for length in range(1, 4):
                if start + length > len(s):
                    break

                segment = s[start:start + length]

                # Leading zeros are not allowed
                if len(segment) > 1 and segment[0] == '0':
                    continue

                # Each segment must be between 0 and 255
                if int(segment) > 255:
                    continue

                parts.append(segment)
                backtrack(start + length, parts)
                parts.pop()

        # An IP address has 4 parts, each containing 1–3 digits
        if 4 <= len(s) <= 12:
            backtrack(0, [])

        return result

```

---

[View on LeetCode](https://leetcode.com/problems/restore-ip-addresses/)