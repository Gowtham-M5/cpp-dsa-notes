# LeetCode 26 — Remove Duplicates from Sorted Array

## Problem
Remove duplicates in place from a sorted array. Return `k`, the number of unique values. The first `k` positions must contain the unique values in sorted order.

## My approach: Two pointers
Because the array is sorted, duplicate values are next to each other.
- `i` scans the array starting from index 1.
- `k` is the next position for a new unique value. It starts at 1 because the first element is already unique.
- Compare `nums[i]` with `nums[k - 1]`, the last unique value.
- If they are different, write `nums[i]` at `nums[k]` and increase `k`.
- Return `k`.

## Code I practised
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k = 1;
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] != nums[k - 1]) {
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
};
```

## Example
Input: `[1,1,2,2,3]`

- Start with `k = 1`.
- Skip the second `1`, because it equals `nums[k - 1]`.
- Keep `2` and then `3) by writing each at index `k`.
- The first three positions contain `[1,2,3]`; return `3`.

## Pointer meaning
- `i`: scans the array.
- `k`: next position to write a new unique value.
- `nums[k - 1]`: last unique value already kept.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`

Only the practiced approach is recorded here; no optimized alternative has been added.
