---
layout: post
title: "LeetCode #1 - Merge Sorted Array"
description: "Important Question #1 on LeetCode: Merge Sorted Array"
date: 2025-09-09 10:00:00 +0530
categories: [LEETCODE, IMPORTANT QUESTION 1/150]
tags: [PROGRAMMING, LEETCODE, ARRAY, TWO POINTER, SORTING] 
media_subpath: /assets/img/leetcode
image:
    path: /header.png
    alt: Header image
    height: 50 px
---
## Problem Statement
🔗 [View on LeetCode](https://leetcode.com/problems/merge-sorted-array/?envType=study-plan-v2&envId=top-interview-150)

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should **not** be returned by the function, but instead be stored inside the array `nums1`.  
To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

---

## Examples

**Example 1:**

```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: 
The arrays we are merging are [1,2,3] and [2,5,6].  
The result of the merge is [1,2,2,3,5,6].
```

**Example 2:**

```
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: 
The arrays we are merging are [1] and [].  
The result of the merge is [1].
```

**Example 3:**

```
Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: 
The arrays we are merging are [] and [1].  
The result of the merge is [1].  
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
```

---

## Constraints

- `nums1.length == m + n`  
- `nums2.length == n`  
- `0 <= m, n <= 200`  
- `1 <= m + n <= 200`  
- `-10^9 <= nums1[i], nums2[j] <= 10^9`

---

## Solution: First Approach

```java
import java.util.Arrays;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int index = 0;
        for(int i=0; i<m+n; i++) {
            if(nums1[i] == 0 && i>=m){
                index = i;
                break;
            }
        }

        for(int i=0; i<n; i++){
            nums1[index + i] = nums2[i];
        }

        Arrays.sort(nums1);

        System.out.println(Arrays.toString(nums1));
    }
}
```

### Complexity Analysis

- **Time Complexity:** O((m+n) log(m+n)) due to sorting at the end.  
- **Space Complexity:** O(1), as the sorting is in-place and no extra arrays are used.
- **Note:** Arrays.sort(int[]) uses Dual-Pivot Quicksort (average O(k log k), where k is the array size)

---

## Solution: Second Approach

```java
import java.util.Arrays;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // Initialize pointers for nums1 (last element of its valid part), nums2 (last element),
        // and the position to place the merged element in nums1 (last position of the combined array).
        int p1 = m - 1;
        int p2 = n - 1;
        int p = m + n - 1;

        // Merge elements from the end of both arrays
        while (p1 >= 0 && p2 >= 0) {
            if (nums1[p1] > nums2[p2]) {
                nums1[p] = nums1[p1];
                p1--;
            } else {
                nums1[p] = nums2[p2];
                p2--;
            }
            p--;
        }

        // If there are remaining elements in nums2, copy them to the beginning of nums1.
        // (Elements remaining in nums1 are already in their correct sorted positions).
        while (p2 >= 0) {
            nums1[p] = nums2[p2];
            p2--;
            p--;
        }

        System.out.println(Arrays.toString(nums1));
    }
}
```
### Complexity Analysis

- **Time Complexity:** O(m + n), since each element is processed once.  
- **Space Complexity:** O(1), as we only use pointers without extra data structures.

---
