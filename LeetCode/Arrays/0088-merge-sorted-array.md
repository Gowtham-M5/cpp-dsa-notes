# LeetCode 88 — Merge Sorted Array

## Problem
Merge two sorted arrays into `nums1`. The first `m` elements of `nums1` and all `n` elements of `nums2` are valid; `nums1` has room for all elements.

## My approach: Three pointers from the back
- `i = m - 1): last valid element in `nums1`.
- `j = n - 1`: last element in `nums2`.
- `k = m + n - 1`: last index in `nums1`.

Compare the values at `i` and `j`. Place the larger value at `nums1[k]`, move the source pointer backward, and decrement `k`. If any values remain in `nums2`, copy them into `nums1`.

## Code I wrote
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
}
else {
nums1[k]=nums2[j];
j--;
}
k--;
}
while(j>=0){
nums1[k]=nums2[j];
j--;
}
}
};
```

## Example
`nums1 = [4,5,6,0,0,0]`, `m = 3`; `nums2 = [1,2,3]`, `n = 3`  
Result: `[1,2,3,4,5,6]`

## Why fill from the back?
The back positions are empty, so placing the largest remaining value there avoids overwriting valid values at the beginning of `nums1`.

## Complexity
- Time: `O(m + n)`
- Extra space: `O(1)`
