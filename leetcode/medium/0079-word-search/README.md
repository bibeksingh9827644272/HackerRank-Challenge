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
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.5 MB (beats 29.10%)  
**Submitted:** 2026-09-28T17:39:25.142Z  

```py
class Solution:
    def exist(self, board, word):
        m = len(board)
        n = len(board[0])

        # Frequency pruning
        count = {}
        for row in board:
            for ch in row:
                count[ch] = count.get(ch, 0) + 1

        need = {}
        for ch in word:
            need[ch] = need.get(ch, 0) + 1

        for ch in need:
            if count.get(ch, 0) < need[ch]:
                return False

        # Start from the rarer character
        if count.get(word[0], 0) > count.get(word[-1], 0):
            word = word[::-1]

        length = len(word)

        def dfs(r, c, i):
            if i == length:
                return True

            if r < 0 or r >= m or c < 0 or c >= n:
                return False

            if board[r][c] != word[i]:
                return False

            # Mark visited
            temp = board[r][c]
            board[r][c] = '#'

            # Search four directions
            if (dfs(r + 1, c, i + 1) or
                dfs(r - 1, c, i + 1) or
                dfs(r, c + 1, i + 1) or
                dfs(r, c - 1, i + 1)):
                
                board[r][c] = temp
                return True

            # Backtrack
            board[r][c] = temp
            return False

        # Try every starting cell
        for r in range(m):
            for c in range(n):
                if board[r][c] == word[0]:
                    if dfs(r, c, 0):
                        return True

        return False
```

---

[View on LeetCode](https://leetcode.com/problems/word-search/)