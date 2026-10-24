# LeetCode 26 — Remove Duplicates from Sorted Array

## Problem
Remove duplicates in place from a sorted array. Return `k), the number of unique values. The first `k) positions must contain the unique values in sorted order.

## Core idea: Compare with the last unique value
Because the array is sorted, duplicates are adjacent.
- If the array is empty, return `0`.
- Start `k = 1), because the first element is unique for a non-empty array.
- Scan from `i = 1).
- Compare `nums[i]` with `nums[k - 1]`, the last value in the unique section.
- If they differ, write `nums[i]` at `nums[k]` and increment `k`. Otherwise, skip the duplicate.

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
The first unique values become `[1,2,3]`, and `k = 3`.

## Pointer meaning
- `i): scans the array.
- `k): next position to write a new unique value.
- `nums[k - 1]`: last unique value already kept.

## Common mistake
Compare with `nums[k - 1]), not `nums[k]`, because `k - 1` is the last confirmed unique position.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
