# Word Search

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given an `m x n` grid of characters `board` and a string `word`, return `true`  *if*  `word`  *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

 **Example 1:** 

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true

```

 **Example 2:** 

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true

```

 **Example 3:** 

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false

```

 

 **Constraints:** 

- m == board.length
- n = board[i].length
- 1 <= m, n <= 6
- 1 <= word.length <= 15
- board and word consists of only lowercase and uppercase English letters.

 

 **Follow up:**  Could you use search pruning to make your solution faster with a larger `board`?

## Solution

**Language:** Python  
**Runtime:** 2 ms (beats 98.13%)  
**Memory:** 19.4 MB (beats 59.76%)  
**Submitted:** 2026-09-28T17:40:36.557Z  

```py
class Solution:
    def exist(self, board, word):
        m, n = len(board), len(board[0])

        # Count characters in board
        freq = {}
        for row in board:
            for ch in row:
                freq[ch] = freq.get(ch, 0) + 1

        # Pruning: check whether word is possible
        required = {}
        for ch in word:
            required[ch] = required.get(ch, 0) + 1

        for ch, count in required.items():
            if freq.get(ch, 0) < count:
                return False

        # Start from the rarer end
        if freq[word[0]] > freq[word[-1]]:
            word = word[::-1]

        length = len(word)

        def dfs(r, c, i):
            # All characters matched
            if i == length:
                return True

            # Invalid position
            if r < 0 or r >= m or c < 0 or c >= n:
                return False

            # Wrong / already visited cell
            if board[r][c] != word[i]:
                return False

            # Mark visited
            temp = board[r][c]
            board[r][c] = '#'

            next_i = i + 1

            # Search in 4 directions
            found = (
                dfs(r + 1, c, next_i) or
                dfs(r - 1, c, next_i) or
                dfs(r, c + 1, next_i) or
                dfs(r, c - 1, next_i)
            )

            # Backtrack
            board[r][c] = temp

            return found

        # Try every possible starting position
        for r in range(m):
            for c in range(n):
                if board[r][c] == word[0]:
                    if dfs(r, c, 0):
                        return True

        return False
```

---

[View on LeetCode](https://leetcode.com/problems/word-search/)