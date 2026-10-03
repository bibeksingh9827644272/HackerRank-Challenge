# Balanced Binary Tree

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

Given a binary tree, determine if it is  **height-balanced**.

 

 **Example 1:** 

```
Input: root = [3,9,20,null,null,15,7]
Output: true

```

 **Example 2:** 

```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false

```

 **Example 3:** 

```
Input: root = []
Output: true

```

 

 **Constraints:** 

- The number of nodes in the tree is in the range [0, 5000].
- -104 <= Node.val <= 104

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 20.3 MB (beats 70.87%)  
**Submitted:** 2026-10-03T13:36:16.272Z  

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root):
        def height(node):
            # Empty tree has height 0
            if node is None:
                return 0

            # Find height of left subtree
            left = height(node.left)

            # If left subtree is unbalanced
            if left == -1:
                return -1

            # Find height of right subtree
            right = height(node.right)

            # If right subtree is unbalanced
            if right == -1:
                return -1

            # Difference in heights must be at most 1
            if abs(left - right) > 1:
                return -1

            # Return height of current node
            return max(left, right) + 1

        return height(root) != -1
```

---

[View on LeetCode](https://leetcode.com/problems/balanced-binary-tree/)