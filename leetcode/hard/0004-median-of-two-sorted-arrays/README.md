# Median of Two Sorted Arrays

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return  **the median**  of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

 

 **Example 1:** 

```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.

```

 **Example 2:** 

```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

```

 

 **Constraints:** 

- nums1.length == m
- nums2.length == n
- 0 <= m <= 1000
- 0 <= n <= 1000
- 1 <= m + n <= 2000
- -106 <= nums1[i], nums2[i] <= 106

## Solution

**Language:** Python  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 19.8 MB (beats 5.18%)  
**Submitted:** 2026-10-02T10:02:47.715Z  

```py
class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        # Make sure nums1 is the smaller array
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        m = len(nums1)
        n = len(nums2)

        left = 0
        right = m

        while left <= right:
            # Partition nums1
            partition1 = (left + right) // 2

            # Partition nums2
            partition2 = (m + n + 1) // 2 - partition1

            # Left and right values of nums1
            left1 = float('-inf') if partition1 == 0 else nums1[partition1 - 1]
            right1 = float('inf') if partition1 == m else nums1[partition1]

            # Left and right values of nums2
            left2 = float('-inf') if partition2 == 0 else nums2[partition2 - 1]
            right2 = float('inf') if partition2 == n else nums2[partition2]

            # Correct partition found
            if left1 <= right2 and left2 <= right1:

                # Total number of elements is odd
                if (m + n) % 2 == 1:
                    return float(max(left1, left2))

                # Total number of elements is even
                return (max(left1, left2) + min(right1, right2)) / 2

            # nums1 partition is too far right
            elif left1 > right2:
                right = partition1 - 1

            # nums1 partition is too far left
            else:
                left = partition1 + 1
                

        left = 0
        right = m

        while left <= right:
            # Partition nums1
            partition1 = (left + right) // 2

            # Partition nums2
            partition2 = (m + n + 1) // 2 - partition1

            # Values around the partitions
            left1 = float('-inf') if partition1 == 0 else nums1[partition1 - 1]
            right1 = float('inf') if partition1 == m else nums1[partition1]

            left2 = float('-inf') if partition2 == 0 else nums2[partition2 - 1]
            right2 = float('inf') if partition2 == n else nums2[partition2]

            # Correct partition
            if left1 <= right2 and left2 <= right1:

                # Odd total length
                if (m + n) % 2 == 1:
                    return float(max(left1, left2))

                # Even total length
                else:
                    return (max(left1, left2) + min(right1, right2)) / 2

            # Move partition in nums1 to the left
            elif left1 > right2:
                right = partition1 - 1

            # Move partition in nums1 to the right
            else:
                left = partition1 + 1
```

---

[View on LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/)