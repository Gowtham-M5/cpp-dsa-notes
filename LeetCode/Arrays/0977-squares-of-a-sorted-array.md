# LeetCode 977 — Squares of a Sorted Array

- **Difficulty:** Easy
- **Topic:** Arrays
- **Pattern practised:** Array traversal + Bubble Sort
- **Status:** Practised in chat; LeetCode acceptance not yet confirmed

## Problem
Given an integer array sorted in non-decreasing order, square every element and return the squared values in non-decreasing order.

## My approach
1. Traverse the array and replace every element with its square.
2. Use nested loops to compare adjacent elements.
3. If `nums[j]` is greater than `nums[j + 1]`, swap them.
4. Repeat the passes so the array becomes sorted.

## Code I wrote
This is the Bubble Sort approach I practised. It does not use the optimized two-pointer method.

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {

       for(int i=0;i<nums.size();i++){
        nums[i]=nums[i]*nums[i];
       } 
       for (int i = 0; i < nums.size() - 1; i++) {
           for (int j = 0; j < nums.size() - 1 - i; j++) {
               if (nums[j] > nums[j + 1]) {
                   swap(nums[j], nums[j + 1]);
               }
           }
       }
       return nums;
    }
};
```

## Example
Input: `[-4,-1,0,3,10]`

After squaring: `[16,1,0,9,100]`

After Bubble Sort: `[0,1,9,16,100]`

## Concepts practised
- `nums.size()` to get the vector size.
- `nums[i] = nums[i] * nums[i]` to square a value.
- `swap(nums[j], nums[j + 1])` to exchange adjacent values.
- Nested loops to make multiple passes through the array.
- The inner loop uses `nums.size() - 1 - i) because the largest values settle at the end after each pass.

## Complexity
- Squaring: `O(n)`
- Bubble Sort: `O(n^2)` time
- Overall time: `O(n^2)`

## Next learning step
The two-pointer approach can solve this problem in `O(n)` time, but it is not included here because I have not practised that solution yet.
