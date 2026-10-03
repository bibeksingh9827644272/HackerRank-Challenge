# Same Tree

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

 

 **Example 1:** 

```
Input: p = [1,2,3], q = [1,2,3]
Output: true

```

 **Example 2:** 

```
Input: p = [1,2], q = [1,null,2]
Output: false

```

 **Example 3:** 

```
Input: p = [1,2,1], q = [1,1,2]
Output: false

```

 

 **Constraints:** 

- The number of nodes in both trees is in the range [0, 100].
- -104 <= Node.val <= 104

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.1 MB (beats 94.85%)  
**Submitted:** 2026-10-03T13:35:10.117Z  

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p, q):
        # Both nodes are empty
        if p is None and q is None:
            return True

        # One node is empty, but the other is not
        if p is None or q is None:
            return False

        # Values are different
        if p.val != q.val:
            return False

        # Check left and right subtrees
        return self.isSameTree(p.left, q.left) and \
               self.isSameTree(p.right, q.right)
```

---

[View on LeetCode](https://leetcode.com/problems/same-tree/)