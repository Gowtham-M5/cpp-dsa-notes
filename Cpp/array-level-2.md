# Array Level 2 — Learning Notes (Original Code First)

**Learning date:** 26 October 2026  
**Language:** C++

Machaa, this file is being kept as a record of the code practised during our learning sessions. I will not silently replace your implementations with alternative versions.

**Important note about code accuracy:** The exact code you typed is visible in our recent conversation for the left-rotation reversal solution, and the right-rotation solutions are recorded in your existing LeetCode 189 notes. For earlier Array Level 2 problems, the full original submissions are not all visible in the current conversation context. Rather than falsely label a newly written solution as your code, those sections identify what was learned and leave the original-code slot clearly marked until the exact submission can be recovered.

## Progress checklist

- [x] Reverse an array using two pointers
- [x] Find the second-largest distinct element
- [x] Check whether an array is sorted
- [x] Remove duplicates from a sorted array
- [x] Move zeroes to the end
- [x] Left rotate by one position
- [x] Left rotate by k using a temporary vector
- [x] Right rotate by k using a temporary vector
- [x] Right rotate by k using reversal
- [x] Left rotate by k using reversal

---

## 1. Reverse an array using two pointers

**What you learned:** Start one pointer at the first index and another at the last. Swap their values and move inward until the pointers meet.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Example:** `[1, 2, 3, 4, 5] → [5, 4, 3, 2, 1]`

- **Time:** O(n)
- **Extra space:** O(1)

## 2. Find the second-largest distinct element

**What you learned:** Find the second-largest value that is different from the largest. Duplicate copies of the largest must not count as the second-largest.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Example:** `[8, 8, 3, 6, 2] → 6`

- **Time:** O(n) for a one-traversal solution
- **Extra space:** O(1)

## 3. Check whether an array is sorted

**What you learned:** Compare neighbouring elements. If an element is smaller than the one before it, the array is not sorted in ascending (non-decreasing) order.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Examples:** `[1, 2, 2, 4] → sorted`; `[1, 4, 3, 5] → not sorted`

- **Time:** O(n) worst case
- **Extra space:** O(1)

## 4. Remove duplicates from a sorted array

**What you learned:** Because equal values are adjacent in a sorted array, use a read position to scan and a write position to keep only new values.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Example:** `[1, 1, 2, 2, 3] → unique prefix [1, 2, 3]`

- **Time:** O(n)
- **Extra space:** O(1)

## 5. Move zeroes to the end

**What you learned:** Move non-zero values forward without changing their relative order, then place zeroes in the remaining positions.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Example:** `[0, 1, 0, 3, 12] → [1, 3, 12, 0, 0]`

- **Time:** O(n)
- **Extra space:** O(1)

## 6. Left rotate by one position

**What you learned:** Save the first value, shift the other values one position left, then put the saved value at the end.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Example:** `[10, 20, 30, 40] → [20, 30, 40, 10]`

- **Time:** O(n)
- **Extra space:** O(1)

## 7. Left rotate by k using a temporary vector

**What you learned:** Save the first k values, move the remaining values left, then copy the saved values to the end. Reduce k with `k %= n` after checking that n is not zero.

**Original code:** The exact submission is not present in the current visible conversation context, so I have not substituted a different implementation here.

**Example:** `[1, 2, 3, 4, 5], k = 2 → [3, 4, 5, 1, 2]`

- **Time:** O(n)
- **Extra space:** O(k)

## 8. Right rotate by k using a temporary vector

**Original code from your existing Rotate Array notes** (same temporary-vector approach, with your saved suffix, backward shift, and copy-back steps):

~~~cpp
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
~~~

**Example:** `[1, 2, 3, 4, 5], k = 2 → [4, 5, 1, 2, 3]`

- **Time:** O(n)
- **Extra space:** O(k)

## 9. Right rotate by k using reversal

**Original code from your existing Rotate Array notes:**

~~~cpp
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
~~~

**Example:** `[1, 2, 3, 4, 5], k = 2 → [4, 5, 1, 2, 3]`

- **Time:** O(n)
- **Extra space:** O(1)

## 10. Left rotate by k using reversal

**Your code from our learning conversation — preserved as written:**

~~~cpp
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
~~~

### Explanation and dry run

For `nums = [1, 2, 3, 4, 5]` and `k = 2`:

1. `reverse(nums, 0, k-1)` reverses the first two values → `[2, 1, 3, 4, 5]`.
2. `reverse(nums, k, n-1)` reverses the rest → `[2, 1, 5, 4, 3]`.
3. `reverse(nums, 0, n-1)` reverses the whole array → `[3, 4, 5, 1, 2]`.

- **Time:** O(n), three reversals together take linear time.
- **Extra space:** O(1), the array is changed in place.

**Important details from your implementation:**
- Check `n == 0` before `k %= n` to avoid division by zero.
- `k %= n` handles k equal to or larger than n.
- The second reversal begins at index `k`, not `k + 1`.
- The order of reversal operations is different for left and right rotation.

---

## Revision summary

- Two pointers: reverse from both ends.
- Read/write pointers: remove duplicates and move zeroes in place.
- Rotations with temporary storage: save the moved part, shift, copy back.
- Right rotation with reversal: reverse all → reverse first k → reverse the rest.
- Left rotation with reversal: reverse first k → reverse the rest → reverse all.

**Note:** The code for Problems 1–7 is intentionally not replaced with a new implementation here. To preserve your exact code, those submissions need to be retrieved from the original learning messages or supplied again if they are no longer available in the conversation context.
