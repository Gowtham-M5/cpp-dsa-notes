# LeetCode 1480 — Running Sum of 1D Array

## Problem
Return an array where each position contains the sum of the original array from index 0 through that position.

## Core idea
Keep a running total. Add the current element to the total, then replace the current element with that cumulative total.

## Code from my practiced solution
```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            nums[i] = sum;
        }
        return nums;
    }
};
```

## Example
Input: `[1,2,3,4]`  
Running totals: `1, 3, 6, 10`  
Output: `[1,3,6,10]`

## Important detail
This solution updates the input vector directly. Each element becomes the running sum up to that index.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
