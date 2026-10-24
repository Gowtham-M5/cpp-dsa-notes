# LeetCode 283 — Move Zeroes

## Problem
Move all zeroes to the end of the array while keeping the relative order of non-zero elements unchanged. Modify the array in place.

## Key idea: Write non-zero values first
Use `j` as the next position where a non-zero value should be written.
1. Scan the array with `i`.
2. Whenever `nums[i] != 0`, copy it to `nums[j]` and increment `j`.
3. After the scan, fill every position from `j` to the end with zeroes.

## C++ solution
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int j = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != 0) {
                nums[j] = nums[i];
                j++;
            }
        }

        while (j < nums.size()) {
            nums[j] = 0;
            j++;
        }
    }
};
```

## Example
Input: `[0,1,0,3,12]`

- Write 1 at index 0
- Write 3 at index 1
- Write 12 at index 2
- Fill the remaining positions with zeroes

Output: `[1,3,12,0,0]`

## Pointer meaning
- `i`: scans every original array position.
- `j`: points to the next write position for a non-zero value.

## Common mistakes
- Forgetting to fill the remaining positions with zeroes.
- Incrementing `j` when the current value is zero.
- Changing the relative order of non-zero values.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
