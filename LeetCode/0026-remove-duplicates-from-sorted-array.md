# LeetCode 26 — Remove Duplicates from Sorted Array

## Problem
Given a sorted array, remove duplicates in place so each distinct value appears once. Return `k`, the number of unique values. The first `k` positions must contain the unique values in sorted order.

## Key idea: Compare with the last unique value
Because the array is sorted, duplicates appear next to each other.
- Start `k = 1), since the first element is unique when the array is non-empty.
- Scan from `i = 1`.
- Compare `nums[i]` with `nums[k - 1]`, the last value written to the unique section.
- If they differ, write `nums[i]` at `nums[k]` and increment `k`.
- If they are equal, skip the duplicate.

## C++ solution
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0;

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

- First 1 is kept; the next 1 matches the last unique value, so skip it.
- 2 differs from the last unique value 1, so write 2 next.
- The second 2 is skipped.
- 3 differs from 2, so write 3 next.

The first `k = 3` values are `[1,2,3]`.

## Pointer meaning
- `i`: scans the original array.
- `k`: length of the unique section and the next write position.
- `nums[k - 1]`: last unique value already kept.

## Common mistake
Use `nums[i]`, not `num[i]`. Also, compare against `nums[k - 1]), not `nums[k]`, because `k - 1` is the last confirmed unique position.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
