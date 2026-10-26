# LeetCode 88 — Merge Sorted Array

## Problem
Merge two sorted arrays into `nums1`. The first `m` elements of `nums1` and all `n` elements of `nums2` are valid; `nums1` has room for all elements.

## Approach practised
Use three pointers to merge from the back:
- `i = m - 1`: last valid element in `nums1`.
- `j = n - 1`: last element in `nums2`.
- `k = m + n - 1`: last index in `nums1`.

Compare the values at `i` and `j`. Put the larger value at `nums1[k]), then move the pointer for the value used backward. Filling from the back avoids overwriting the valid elements at the beginning of `nums1`.

If any values remain in `nums2`, they must be copied into `nums1`.

## Example
`nums1 = [4,5,6,0,0,0]`, `m = 3`  
`nums2 = [1,2,3]`, `n = 3`

Result: `[1,2,3,4,5,6]`

## Learning from debugging
An earlier attempt produced an incorrect array because values in `nums1` were overwritten before they were safely placed. Working backward prevents that problem.

## Code note
The code previously saved here was not verified as the exact code I personally wrote. It has been removed rather than presenting an assistant-written implementation as mine. Add my own accepted code after I retype or retry it.

## Complexity
- Time: `O(m + n)`
- Extra space: `O(1)`
