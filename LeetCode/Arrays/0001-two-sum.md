# LeetCode 1 — Two Sum

## Problem
Given an array and a target, return the indices of two different elements whose values add up to the target.

## Core idea: Check pairs
Use two loops. For each index `i), check later indices `j = i + 1). If `nums[i] + nums[j] == target`, return both indices.

## C++ solution (brute force)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
            }
        }
        return {};
    }
};
```

## What does `return {i, j}` mean?
The function returns a `vector<int>`. The braces create a vector containing the two indices. It returns the answer immediately; it is not a separate function call.

## Example
`nums = [2,7,11,15]`, `target = 9` → return `[0,1]`.

## Complexity
- Time: `O(n^2))
- Extra space: `O(1)), excluding the returned vector.
