# LeetCode 283 — Move Zeroes

## Problem
Move all zeroes to the end while preserving the order of non-zero elements. Modify the array in place.

## Core idea: Write non-zero values first
- `i` scans the array.
- `j` is the next position where a non-zero value should be written.
- Copy each non-zero value to `nums[j]), increment `j), then fill all remaining positions with zeroes.

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
Write the non-zero values first: `[1,3,12,_,_]`  
Fill the remaining positions with zeroes: `[1,3,12,0,0]`

## Common mistakes
- Forgetting to fill remaining positions with zeroes.
- Incrementing `j` when the current value is zero.
- Changing the order of non-zero values.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
