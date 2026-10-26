# LeetCode 1920 — Build Array from Permutation

## Problem
Given an array `nums`, build an answer array such that `ans[i] = nums[nums[i]]`.

## Core idea
Create an answer array with the same number of elements as `nums`. For each index `i), use the value `nums[i]` as an index into `nums`, then store that result at `ans[i]`.

## Example
Input: `nums = [0,2,1,5,3,4]`

- `ans[0] = nums[nums[0]] = nums[0] = 0`
- `ans[1] = nums[nums[1]] = nums[2] = 1`
- Continue the same operation for every index.

Output: `[0,1,2,4,5,3]`.

## Important detail
Allocate the answer array with the required size before assigning values by index.

## Code note
The code previously saved here was not verified as the exact code I personally wrote. It has been removed rather than presenting an assistant-written implementation as mine. Add my own code after retrying the problem.

## Complexity
- Time: `O(n)`
- Extra space: `O(n)`
