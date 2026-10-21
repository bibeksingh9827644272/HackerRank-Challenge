# Merge k Sorted Lists

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

 *Merge all the linked-lists into one sorted linked-list and return it.* 

 

 **Example 1:** 

```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted linked list:
1->1->2->3->4->4->5->6

```

 **Example 2:** 

```
Input: lists = []
Output: []

```

 **Example 3:** 

```
Input: lists = [[]]
Output: []

```

 

 **Constraints:** 

- k == lists.length
- 0 <= k <= 104
- 0 <= lists[i].length <= 500
- -104 <= lists[i][j] <= 104
- lists[i] is sorted in ascending order.
- The sum of lists[i].length will not exceed 104.

## Solution

**Language:** Python  
**Runtime:** 7 ms (beats 83.82%)  
**Memory:** 22.7 MB (beats 73.24%)  
**Submitted:** 2026-10-21T16:48:50.021Z  

```py
class Solution:
    def mergeKLists(self, lists):
        values = []

        for head in lists:
            while head:
                values.append(head.val)
                head = head.next

        values.sort()

        dummy = ListNode(0)
        current = dummy

        for val in values:
            current.next = ListNode(val)
            current = current.next

        return dummy.next
```

---

[View on LeetCode](https://leetcode.com/problems/merge-k-sorted-lists/)