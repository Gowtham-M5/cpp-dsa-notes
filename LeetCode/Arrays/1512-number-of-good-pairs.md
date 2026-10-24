# LeetCode 1512 — Number of Good Pairs

## Problem
Count pairs of indices `(i, j)) where `nums[i] == nums[j]) and `i < j).

## Core idea: Compare each pair once
Use nested loops:
- `i) scans each element.
- `j) starts at `i + 1), so only later elements are checked.
- If the values match, increment the pair count.

## C++ solution
```cpp
class Solution {
public:
    int numIdenticalPairs(vector<int>& nums) {
        int count = 0;

        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] == nums[j]) {
                    count++;
                }
            }
        }

        return count;
    }
};
```

## Example
Input: `[1,2,3,1,1,3]`  
The matching index pairs are `(0,3)`, `(0,4)`, `(3,4)`, and `(2,5)).  
Output: `4`.

## Common mistake
Start the inner loop at `j = i + 1). This avoids comparing an element with itself and prevents counting the same pair twice.

## Complexity
- Time: `O(n^2))
- Extra space: `O(1)`
