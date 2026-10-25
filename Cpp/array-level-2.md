# Array Level 2 — Complete Notes & Solutions

**Learning date:** 26 October 2026  
**Language:** C++  
**Goal:** Build strong array problem-solving skills for placements and DSA interviews.

These are general array practice problems, not necessarily LeetCode questions. Each section includes the intuition, complete C++ code, example/dry run, complexity, and common mistakes.

## Progress checklist

- [x] 1. Reverse an array using two pointers
- [x] 2. Find the second-largest distinct element
- [x] 3. Check whether an array is sorted
- [x] 4. Remove duplicates from a sorted array
- [x] 5. Move all zeroes to the end
- [x] 6. Left rotate an array by one position
- [x] 7. Left rotate by k using a temporary vector
- [x] 8. Right rotate by k using a temporary vector
- [x] 9. Right rotate by k using reversal
- [x] 10. Left rotate by k using reversal

---

## Common setup

The snippets below use `vector<int>` and `swap`. For a standalone program, include:

~~~cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
~~~

The functions can be used inside `main()` or a solution class. Rotation functions modify the vector passed by reference.

## 1. Reverse an Array — Two Pointers

### Intuition
Place one pointer at the start and another at the end. Swap those values, move the left pointer forward and the right pointer backward, and stop when they meet or cross.

### Complete code
~~~cpp
void reverseArray(vector<int>& nums) {
    int left = 0;
    int right = static_cast<int>(nums.size()) - 1;

    while (left < right) {
        swap(nums[left], nums[right]);
        left++;
        right--;
    }
}
~~~

### Example and dry run
Input: `[1, 2, 3, 4, 5]`

- Swap indices 0 and 4: `[5, 2, 3, 4, 1]`
- Swap indices 1 and 3: `[5, 4, 3, 2, 1]`
- Both pointers meet around the middle; stop.

Output: `[5, 4, 3, 2, 1]`

- **Time:** O(n), because each element is involved in at most one swap.
- **Extra space:** O(1), because only two indices and a swap temporary are used.

**Common mistakes:** The last valid index is `size() - 1), not `size()`. Empty vectors are safe here because `right` becomes -1 and the loop does not run.

## 2. Find the Second-Largest Distinct Element

### Intuition
Track the largest and second-largest values while scanning once. “Distinct” means the second-largest must be strictly smaller than the largest. Duplicate copies of the largest must not become the answer.

### Complete code
This version uses flags rather than a numeric sentinel, so it also works when values can be `INT_MIN`.

~~~cpp
#include <optional>

optional<int> secondLargestDistinct(const vector<int>& nums) {
    bool hasLargest = false;
    bool hasSecond = false;
    int largest = 0;
    int second = 0;

    for (int value : nums) {
        if (!hasLargest || value > largest) {
            if (hasLargest) {
                second = largest;
                hasSecond = true;
            }
            largest = value;
            hasLargest = true;
        } else if (value < largest && (!hasSecond || value > second)) {
            second = value;
            hasSecond = true;
        }
    }

    if (hasSecond) return second;
    return nullopt;
}
~~~

For this version, include `<optional>` and use C++17 or later. If no second distinct value exists, the function returns `nullopt`.

### Example and dry run
Input: `[8, 8, 3, 6, 2]`

- First 8: largest = 8.
- Second 8: it is equal to largest, so ignore it.
- 3: second = 3.
- 6: 6 is below 8 but above 3, so second = 6.
- 2: it does not change either value.

Output: `6`.

- **Time:** O(n), one traversal.
- **Extra space:** O(1), fixed number of variables.

**Common mistakes:** Do not treat a duplicate largest value as second-largest. Check arrays such as `[5, 5]`, `[-4, -2, -9]`, and an empty array.

## 3. Check Whether an Array Is Sorted in Ascending Order

### Intuition
Compare every element with its previous element. If an element is smaller than the previous one, the array is not sorted. Equal adjacent elements are allowed, so this checks non-decreasing order.

### Complete code
~~~cpp
bool isSorted(const vector<int>& nums) {
    for (int i = 1; i < static_cast<int>(nums.size()); i++) {
        if (nums[i] < nums[i - 1]) {
            return false;
        }
    }
    return true;
}
~~~

### Example and dry run
Input: `[1, 2, 2, 4]`

- 2 is not less than 1.
- 2 is not less than 2.
- 4 is not less than 2.
- No descending pair was found, so return `true`.

Input: `[1, 4, 3, 5]` returns `false) when 3 is compared with 4.

- **Time:** O(n) worst case; it may return earlier if an inversion is found.
- **Extra space:** O(1).

**Common mistakes:** Start at index 1 because index 0 has no previous element. An empty or one-element vector is considered sorted.

## 4. Remove Duplicates from a Sorted Array

### Intuition
Because the input is sorted, duplicates are next to one another. Keep a write index for the next unique value. Scan the array and write a value only when it differs from the last unique value.

### Complete code
The function returns the number of unique values. They occupy the first `k` positions; values after that prefix are not part of the result.

~~~cpp
int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;

    int write = 1;

    for (int read = 1; read < static_cast<int>(nums.size()); read++) {
        if (nums[read] != nums[write - 1]) {
            nums[write] = nums[read];
            write++;
        }
    }

    return write;
}
~~~

### Example and dry run
Input: `[1, 1, 2, 2, 3]`

- Start with `write = 1); the first 1 is already the first unique value.
- Read the second 1: same as the previous unique value, so skip it.
- Read 2: new value; write it at index 1.
- Read the next 2: skip it.
- Read 3: new value; write it at index 2.

The first `k = 3` values are `[1, 2, 3]`.

- **Time:** O(n).
- **Extra space:** O(1).

**Common mistakes:** This method assumes the input is sorted. Do not assume the vector's physical size becomes `k`; the returned length tells you which prefix contains the answer.

## 5. Move All Zeroes to the End

### Intuition
Move each non-zero value forward in its original order. Then fill every position left over at the end with zero. This preserves the order of the non-zero values and does not need a second vector.

### Complete code
~~~cpp
void moveZeroes(vector<int>& nums) {
    int write = 0;

    for (int value : nums) {
        if (value != 0) {
            nums[write] = value;
            write++;
        }
    }

    while (write < static_cast<int>(nums.size())) {
        nums[write] = 0;
        write++;
    }
}
~~~

### Example and dry run
Input: `[0, 1, 0, 3, 12]`

- Copy 1 to index 0.
- Skip zero.
- Copy 3 to index 1.
- Copy 12 to index 2.
- Fill indices 3 and 4 with zeroes.

Output: `[1, 3, 12, 0, 0]`.

- **Time:** O(n), two linear passes.
- **Extra space:** O(1).

**Common mistakes:** Preserve the order of non-zero values. This function modifies the original vector.

## 6. Left Rotate an Array by One Position

### Intuition
Save the first value because it will be overwritten. Shift all later values one index to the left, then place the saved value at the final index.

### Complete code
~~~cpp
void leftRotateByOne(vector<int>& nums) {
    int n = static_cast<int>(nums.size());
    if (n <= 1) return;

    int first = nums[0];

    for (int i = 0; i < n - 1; i++) {
        nums[i] = nums[i + 1];
    }

    nums[n - 1] = first;
}
~~~

### Example and dry run
Input: `[10, 20, 30, 40]`

- Save 10.
- Move 20 to index 0, 30 to index 1, and 40 to index 2.
- Put saved 10 at index 3.

Output: `[20, 30, 40, 10]`.

- **Time:** O(n).
- **Extra space:** O(1).

**Common mistakes:** Save the first element before shifting; otherwise it is lost. Empty and one-element vectors need no changes.

## 7. Left Rotate by k — Temporary Vector

### Intuition
A left rotation by `k) moves the first `k` values to the end. Save those values, shift the rest to the left, and copy the saved values into the final `k` positions. First reduce `k) modulo the length because rotating by the full length changes nothing.

### Complete code
~~~cpp
void leftRotate(vector<int>& nums, int k) {
    int n = static_cast<int>(nums.size());
    if (n == 0) return;

    k %= n;
    vector<int> temp(nums.begin(), nums.begin() + k);

    for (int i = 0; i < n - k; i++) {
        nums[i] = nums[i + k];
    }

    for (int i = 0; i < k; i++) {
        nums[n - k + i] = temp[i];
    }
}
~~~

### Example and dry run
Input: `[1, 2, 3, 4, 5]), `k = 2)

- Save `[1, 2]`.
- Shift the rest to get `[3, 4, 5, 4, 5]).
- Copy `[1, 2]` to the last two positions.

Output: `[3, 4, 5, 1, 2]`.

- **Time:** O(n).
- **Extra space:** O(k) for the temporary vector.

**Common mistakes:** Check for an empty vector before `k %= n). Reducing `k) handles cases where `k >= n).

## 8. Right Rotate by k — Temporary Vector

### Intuition
A right rotation by `k) moves the last `k) values to the front. Save that suffix, shift the other values to the right, then copy the saved suffix to the front. Shift from right to left so values are not overwritten before being copied.

### Complete code
~~~cpp
void rightRotate(vector<int>& nums, int k) {
    int n = static_cast<int>(nums.size());
    if (n == 0) return;

    k %= n;
    vector<int> temp(nums.end() - k, nums.end());

    for (int i = n - 1; i >= k; i--) {
        nums[i] = nums[i - k];
    }

    for (int i = 0; i < k; i++) {
        nums[i] = temp[i];
    }
}
~~~

### Example and dry run
Input: `[1, 2, 3, 4, 5]), `k = 2)

- Save the last two values: `[4, 5]`.
- Shift `[1, 2, 3]` two positions to the right.
- Copy `[4, 5]` to the front.

Output: `[4, 5, 1, 2, 3]`.

- **Time:** O(n).
- **Extra space:** O(k).

**Common mistakes:** Iterate backward during the right shift. If `k = 0), the temporary vector is empty and the loops leave the array unchanged.

## 9. Right Rotate by k — Reversal Algorithm

### Intuition
Three reversals move the final `k) elements to the front:
1. Reverse the entire array.
2. Reverse the first `k) elements.
3. Reverse the remaining elements.

### Complete code
~~~cpp
void reverseRange(vector<int>& nums, int left, int right) {
    while (left < right) {
        swap(nums[left], nums[right]);
        left++;
        right--;
    }
}

void rightRotateByReversal(vector<int>& nums, int k) {
    int n = static_cast<int>(nums.size());
    if (n == 0) return;

    k %= n;

    reverseRange(nums, 0, n - 1);
    reverseRange(nums, 0, k - 1);
    reverseRange(nums, k, n - 1);
}
~~~

### Example and dry run
Input: `[1, 2, 3, 4, 5]), `k = 2)

1. Reverse all → `[5, 4, 3, 2, 1]`.
2. Reverse first two → `[4, 5, 3, 2, 1]`.
3. Reverse indices 2 through 4 → `[4, 5, 1, 2, 3]`.

- **Time:** O(n), since the three reversals together do linear work.
- **Extra space:** O(1), because all changes happen in place.

**Common mistakes:** Do not reverse the first `k) elements before reversing the whole array for this right-rotation order. Keep the empty-vector check before modulo.

## 10. Left Rotate by k — Reversal Algorithm

### Intuition
For left rotation, the first `k) values must move to the end:
1. Reverse the first `k) elements.
2. Reverse the remaining elements.
3. Reverse the entire array.

### Complete code
~~~cpp
void leftRotateByReversal(vector<int>& nums, int k) {
    int n = static_cast<int>(nums.size());
    if (n == 0) return;

    k %= n;

    reverseRange(nums, 0, k - 1);
    reverseRange(nums, k, n - 1);
    reverseRange(nums, 0, n - 1);
}
~~~

This reuses the `reverseRange` helper from Problem 9. Keep only one copy of that helper in a single source file.

### Example and dry run
Input: `[1, 2, 3, 4, 5]), `k = 2)

1. Reverse first two → `[2, 1, 3, 4, 5]`.
2. Reverse the remaining values → `[2, 1, 5, 4, 3]`.
3. Reverse all → `[3, 4, 5, 1, 2]`.

Another example: `[10, 20, 30, 40, 50, 60]), `k = 3) → `[40, 50, 60, 10, 20, 30]`.

- **Time:** O(n).
- **Extra space:** O(1).

**Common mistakes:** The second reversal starts at index `k), not `k + 1). Left and right rotation use different reversal orders.

---

## Quick comparison

| Problem/approach | Main pattern | Time | Extra space |
|---|---|---:|---:|
| Reverse array | Two pointers | O(n) | O(1) |
| Second-largest distinct | Track two best values | O(n) | O(1) |
| Check sorted | Compare neighbours | O(n) worst case | O(1) |
| Remove duplicates | Read/write pointers | O(n) | O(1) |
| Move zeroes | Read/write pointer, then fill | O(n) | O(1) |
| Left rotate by one | Save and shift | O(n) | O(1) |
| Left rotate by k, temporary vector | Save prefix and shift | O(n) | O(k) |
| Right rotate by k, temporary vector | Save suffix and shift backward | O(n) | O(k) |
| Right rotate by k, reversal | Three reversals | O(n) | O(1) |
| Left rotate by k, reversal | Three reversals | O(n) | O(1) |

## Important habits to remember

1. **Understand the input assumption.** Removing adjacent duplicates this way requires a sorted array.
2. **Check edge cases.** Empty vector, one element, all equal values, `k = 0), and `k) larger than the vector size.
3. **Avoid modulo by zero.** Always check `n == 0` before `k %= n`.
4. **Use the right loop direction.** When shifting right, work backward to avoid overwriting values you still need.
5. **Know the result format.** In remove-duplicates problems, the return value `k` is the length of the valid unique prefix.
6. **Know the space trade-off.** Temporary vectors are easy to understand but use O(k) additional storage; reversal uses O(1) extra space.
