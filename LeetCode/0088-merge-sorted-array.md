# LeetCode 88 — Merge Sorted Array

## Problem
Given sorted arrays `nums1` and `nums2`, merge `nums2` into `nums1` in sorted order. The first array has enough extra space at the end to hold all elements.

## Key idea: Fill from the back
The first `m` values of `nums1` and all `n` values of `nums2` are valid. Use three pointers:
- `i = m - 1`: last valid element in `nums1`
- `j = n - 1`: last element in `nums2`
- `k = m + n - 1`: last position in `nums1`

Compare `nums1[i]` and `nums2[j]`. Put the larger value at `nums1[k]`, then move the corresponding pointer backward and decrement `k`. When `nums2` still has values, copy them into `nums1`.

## C++ solution
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                i--;
            } else {
                nums1[k] = nums2[j];
                j--;
            }
            k--;
        }

        while (j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
    }
};
```

## Example
`nums1 = [4,5,6,0,0,0], m = 3`  
`nums2 = [1,2,3], n = 3`

Compare from the end:
- 6 is largest → place at index 5
- 5 is larger than 3 → place at index 4
- 4 is larger than 3 → place at index 3
- Copy remaining 3, 2, 1 into the first three positions

Result: `[1,2,3,4,5,6]`

## Why start from the end?
Writing from the front could overwrite valid values in `nums1` before we use them. Filling from the back preserves the original values we still need.

## Common mistake
Do not compare or copy all `nums1.size()` elements as if they were valid. Only the first `m` elements are valid initially. Also, if `nums2` becomes empty, the remaining `nums1` values are already in place.

## Complexity
- Time: `O(m + n)`
- Extra space: `O(1)`
