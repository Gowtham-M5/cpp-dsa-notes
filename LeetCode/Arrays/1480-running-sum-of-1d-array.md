# LeetCode 1480 — Running Sum of 1D Array

## Problem
Return an array where each position contains the sum of the original array from index 0 through that position.

## Core idea
Keep a running total. Add the current element to the total, then store that total in the answer array.

## C++ solution
```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        vector<int> ans(nums.size());
        int sum = 0;

        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            ans[i] = sum;
        }

        return ans;
    }
};
```

## Example
Input: `[1,2,3,4]`  
Running totals: `1, 1+2=3, 1+2+3=6, 1+2+3+4=10`  
Output: `[1,3,6,10]`

## Common mistake
Create the answer vector with the required size before assigning values by index. An empty vector cannot safely be assigned to using `ans[i]` until elements have been added or space has been allocated.

## Complexity
- Time: `O(n)`
- Extra space: `O(n)` for the answer array.
