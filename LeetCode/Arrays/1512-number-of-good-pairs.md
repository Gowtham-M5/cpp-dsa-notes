# LeetCode 1512 — Number of Good Pairs

## Problem
Count pairs of indices `(i, j)` where `nums[i] == nums[j]` and `i < j`.

## Core idea: Compare each pair once
Use nested loops. The inner loop starts at `j = i + 1`, so each element is compared only with elements after it. If the values match, increase `goodpairs`.

## Code I wrote
```cpp
class Solution {
public:
    int numIdenticalPairs(vector<int>& nums) {
        int goodpairs = 0;
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] == nums[j]) {
                    goodpairs++;
                }
            }
        }
        return goodpairs;
    }
};
```

## Example
Input: `[1,2,3,1,1,3]`

Matching pairs: `(0,3)`, `(0,4)`, `(2,5)`, and `(3,4)`.  
Output: `4`.

## Common mistake
Starting `j` at `i + 1` avoids comparing an element with itself and prevents counting the same pair twice.

## Complexity
- Time: `O(n^2)`
- Extra space: `O(1)`
