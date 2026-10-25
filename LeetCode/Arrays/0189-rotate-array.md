# LeetCode 189 — Rotate Array

- **Difficulty:** Medium
- **Topic:** Arrays
- **Pattern:** Temporary Array + Backward Shifting
- **Status:** Solved — Accepted

## Problem

Given an integer array `nums`, rotate the array to the right by `k` steps.

### Example

```text
Input:  nums = [1,2,3,4,5,6,7], k = 3
Output:       [5,6,7,1,2,3,4]
```

## Approach

1. Let `n = nums.size()`.
2. Use `k = k % n` so that rotations larger than the array length are handled. If `k == 0`, the array does not need to change.
3. Store the last `k` elements in a temporary vector.
4. Shift the remaining elements `k` positions to the right, starting at the last index and moving backward.
5. Copy the saved elements to the beginning of `nums`.

## C++ Solution

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        if (n == 0) return;

        k %= n;
        vector<int> temp(k);

        // Step 1: Store the last k elements
        for (int i = 0; i < k; i++) {
            temp[i] = nums[n - k + i];
        }

        // Step 2: Shift the remaining elements right by k positions
        for (int i = n - 1; i >= k; i--) {
            nums[i] = nums[i - k];
        }

        // Step 3: Copy the saved elements to the beginning
        for (int i = 0; i < k; i++) {
            nums[i] = temp[i];
        }
    }
};
```

## Dry Run

Input: `nums = [1,2,3,4,5,6,7]`, `k = 3`

### Step 1 — Save the last 3 elements

```text
nums = [1,2,3,4,5,6,7]
temp = [5,6,7]
```

The temporary vector stores the elements that must move to the beginning.

### Step 2 — Shift right, moving backward

The loop is `for (int i = n - 1; i >= k; i--)` and performs `nums[i] = nums[i-k]`.

| i | Assignment | Array after assignment |
|---:|---|---|
| 6 | nums[6] = nums[3] (4) | [1,2,3,4,5,6,4] |
| 5 | nums[5] = nums[2] (3) | [1,2,3,4,5,3,4] |
| 4 | nums[4] = nums[1] (2) | [1,2,3,4,2,3,4] |
| 3 | nums[3] = nums[0] (1) | [1,2,3,1,2,3,4] |

**Why move backward?** Moving backward prevents us from overwriting values that still need to be copied to a later position.

### Step 3 — Copy temp to the beginning

- `nums[0] = temp[0]` → [5,2,3,1,2,3,4]
- `nums[1] = temp[1]` → [5,6,3,1,2,3,4]
- `nums[2] = temp[2]` → [5,6,7,1,2,3,4]

Final result: `[5,6,7,1,2,3,4]`

## Key Concepts Learned

- **Temporary storage:** Save elements before modifying the array.
- **Backward traversal:** Start at the end when shifting right to avoid overwriting values that are still needed.
- **Modulo (`%`):** `k % n` reduces unnecessary full rotations.
- **Indexing:** The last `k` elements start at index `n - k`.

## Complexity

- **Time:** O(n) — each loop processes at most the array length.
- **Extra space:** O(k) — the temporary vector stores `k` elements.

## Common Mistakes to Avoid

- Saving the first `k` elements instead of the last `k` for a right rotation.
- Shifting forward and overwriting elements before they are copied.
- Using `k` directly when it can be larger than `n`; reduce it with `k %= n`.
- Using the rotation count `k` as a loop variable and accidentally changing it.
- Performing `k % n` before checking whether `n` is zero.

## Pattern Summary

**Save → Shift backward → Copy.**

This is the temporary-storage approach to array rotation. Another common solution uses three reversals and O(1) extra space.
