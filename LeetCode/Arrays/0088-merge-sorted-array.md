# LeetCode 88 — Merge Sorted Array

## Problem
Merge two sorted arrays into `nums1`. The first `m` elements of `nums1` and all `n` elements of `nums2` are valid; `nums1` has room for all elements.

## Core idea: Fill from the back
Use three pointers:
- `i = m - 1`: last valid element in `nums1`
- `j = n - 1`: last element in `nums2`
- `k = m + n - 1`: last index in `nums1`

Compare `nums1[i]` and `nums2[j]`. Put the larger value at `nums1[k]`, move that source pointer backward, and decrement `k`. If any values remain in `nums2`, copy them into `nums1`.

## C++ solution
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }

        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
};
```

## Example
`nums1 = [4,5,6,0,0,0]`, `m = 3`; `nums2 = [1,2,3]`, `n = 3`  
Result: `[1,2,3,4,5,6]`

## Why fill from the back?
Filling from the front could overwrite valid values in `nums1). The back positions are empty, so we can safely place the largest remaining value there.

## Common mistake
Only the first `m` elements of `nums1` are initially valid. If `nums2` becomes empty, the remaining `nums1` elements are already in the correct place.

## Complexity
- Time: `O(m + n)`
- Extra space: `O(1)`
