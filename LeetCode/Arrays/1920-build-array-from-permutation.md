# LeetCode 1920 — Build Array from Permutation

## Problem
Given an array `nums`, build an answer array such that `ans[i] = nums[nums[i]]`.

## Core idea
Create an answer vector with the same size as `nums`. For every index `i`, use `nums[i]` as an index into `nums` and store that value in `ans[i]`.

## Code I wrote
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
Input: `nums = [0,2,1,5,3,4]`  
Output: `[0,1,2,4,5,3]`

For example, `ans[1] = nums[nums[1]] = nums[2] = 1`.

## Important detail
`vector<int> ans(nums.size())` creates an answer vector with the required number of positions before assigning values by index.

## Complexity
- Time: `O(n)`
- Extra space: `O(n)`
