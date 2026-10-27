# LeetCode 189 — Rotate Array

- **Difficulty:** Medium
- **Topic:** Arrays
- **Pattern:** Three Reversals
- **Status:** Solved — Accepted

## Problem
Given an integer array `nums`, rotate the array to the right by `k` steps.

### Example
```text
Input:  nums = [1,2,3,4,5,6,7], k = 3
Output:       [5,6,7,1,2,3,4]
```

## My approach: Three reversals
1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the remaining elements from index `k` to `n - 1`.

Reversing the entire array brings the last `k` elements to the front, but both parts are reversed. Reversing each part separately restores their correct order.

## Code I practised
```cpp
class Solution {
public:
    void reverse(vector<int>& nums, int left, int right) {
        while (left < right) {
            swap(nums[left], nums[right]);
            left++;
            right--;
        }
    }

    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        if (n == 0) {
            return;
        }

        k = k % n;

        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }
};
```

## Dry run
Input: `nums = [1,2,3,4,5,6,7]`, `k = 3`

1. Reverse all: `[7,6,5,4,3,2,1]`
2. Reverse first 3: `[5,6,7,4,3,2,1]`
3. Reverse indices 3 through 6: `[5,6,7,1,2,3,4]`

## Key concepts
- `swap(nums[left], nums[right])` exchanges two values.
- Move `left` forward and `right` backward until they meet.
- `k = k % n` handles rotations larger than the array length.
- Check that `n` is not zero before using `k % n`.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
