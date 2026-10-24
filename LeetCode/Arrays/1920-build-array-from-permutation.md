# LeetCode 1920 — Build Array from Permutation

## Problem
Given an array `nums), build `ans) such that `ans[i] = nums[nums[i]]).

## Core idea
Create an answer vector with the same size as `nums). For each index `i), use the value `nums[i]) as an index into `nums), then store that result at `ans[i]).

## C++ solution
```cpp
class Solution {
public:
    vector<int> buildArray(vector<int>& nums) {
        vector<int> ans(nums.size());

        for (int i = 0; i < nums.size(); i++) {
            ans[i] = nums[nums[i]];
        }

        return ans;
    }
};
```

## Example
Input: `nums = [0,2,1,5,3,4])  
- `ans[0] = nums[nums[0]] = nums[0] = 0)
- `ans[1] = nums[nums[1]] = nums[2] = 1)
- Continue for each index.

Output: `[0,1,2,4,5,3]).

## Common mistake
Do not assign `ans[i]) before allocating the answer vector's size. `vector<int> ans(nums.size())) creates the required positions.

## Complexity
- Time: `O(n))
- Extra space: `O(n))
