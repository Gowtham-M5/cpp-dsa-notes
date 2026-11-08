# 10. Left Rotate by k — Reversal Algorithm

## Intuition
For left rotation, the first k values need to move to the end. Reverse the first part, reverse the second part, and finally reverse the whole array.

## Your C++ code
This implementation is preserved from your learning conversation.

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

        reverse(nums, 0, k-1);
        reverse(nums, k, n - 1);
        reverse(nums, 0, n-1 );
    }
};
```

## Dry run
Input: `nums = [1, 2, 3, 4, 5]`, `k = 2`

1. Reverse indices 0 to 1 → `[2, 1, 3, 4, 5]`
2. Reverse indices 2 to 4 → `[2, 1, 5, 4, 3]`
3. Reverse indices 0 to 4 → `[3, 4, 5, 1, 2]`

Output: `[3, 4, 5, 1, 2]`

Another check: `[10, 20, 30, 40, 50, 60]`, k = 3 → `[40, 50, 60, 10, 20, 30]`.

## Complexity
- Time: O(n), because the three reversals together process the array linearly.
- Extra space: O(1), because rotation happens in place.

## Common mistakes
- Check for an empty vector before taking `k % n`.
- Reduce k using `k = k % n`.
- The second reversal starts at index k.
- Left and right rotations use different orders of reversal.
