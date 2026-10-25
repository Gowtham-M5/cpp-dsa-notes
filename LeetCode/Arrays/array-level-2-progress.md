# Array Level 2 — Progress & Solutions

**Learning progress updated:** 26 October 2026  
**Language:** C++  
**Status:** Problems covered in our learning sessions are documented below.

This file records the Array Level 2 problems we have practised, the main idea for each one, complexity, and useful C++ patterns.

## Progress checklist

- [x] Reverse an array using two pointers
- [x] Find the second-largest **distinct** element in one traversal
- [x] Check whether an array is sorted in ascending order
- [x] Remove duplicates from a sorted array in place
- [x] Move all zeroes to the end while preserving the order of non-zero elements
- [x] Left rotate an array by one position
- [x] Left rotate an array by k positions using a temporary vector
- [x] Right rotate an array by k positions using a temporary vector
- [x] Right rotate an array by k positions using the reversal algorithm
- [x] Left rotate an array by k positions using the reversal algorithm

---

## 1. Reverse an Array — Two Pointers

**Idea:** Keep one pointer at the beginning and another at the end. Swap the values, then move both pointers toward the middle.

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

**Example:** [1, 2, 3, 4, 5] → [5, 4, 3, 2, 1]

- **Time:** O(n)
- **Extra space:** O(1)

## 2. Find the Second-Largest Distinct Element

**Idea:** Track the largest and second-largest distinct values in one traversal. Only update the second-largest when a value is smaller than the largest but greater than the current second-largest.

**Important:** The second-largest must be distinct from the largest. For example, in [8, 8, 5], the answer is 5, not 8.

- **Time:** O(n)
- **Extra space:** O(1)

**Edge cases:** Fewer than two elements, all values equal, and arrays with no second distinct value. Avoid relying on a sentinel such as INT_MIN without separately tracking whether a second value has been found.

## 3. Check Whether an Array Is Sorted in Ascending Order

**Idea:** Compare each element with the element before it. If any nums[i] < nums[i - 1], the array is not sorted in non-decreasing order.

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

This treats equal adjacent values as sorted: [1, 2, 2, 4] is sorted.

- **Time:** O(n) worst case
- **Extra space:** O(1)

## 4. Remove Duplicates from a Sorted Array

**Idea:** Use two pointers. One pointer scans every element; a write position records where the next new distinct value should go. This works because the input is sorted, so duplicates are adjacent.

For the common in-place problem, the first k positions contain the unique values after the algorithm finishes; k is the new logical length.

- **Time:** O(n)
- **Extra space:** O(1)

**Common mistake:** This approach assumes the array is sorted. For an unsorted array, equal values are not necessarily adjacent.

## 5. Move Zeroes to the End

**Idea:** Copy non-zero values forward in their original order, then fill the remaining positions with zeroes.

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

**Example:** [0, 1, 0, 3, 12] → [1, 3, 12, 0, 0]

- **Time:** O(n)
- **Extra space:** O(1)
- **Key property:** The relative order of non-zero values is preserved.

## 6. Left Rotate by One Position

**Idea:** Save the first element, shift every later element one position to the left, then put the saved value at the end.

**Example:** [1, 2, 3, 4] → [2, 3, 4, 1]

- **Time:** O(n)
- **Extra space:** O(1)

## 7. Left Rotate by k — Temporary Vector

**Idea:** Reduce k using k %= n. Save the first k elements, shift the remaining elements left, and copy the saved elements to the end.

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

**Example:** [1, 2, 3, 4, 5], k = 2 → [3, 4, 5, 1, 2]

- **Time:** O(n)
- **Extra space:** O(k)

## 8. Right Rotate by k — Temporary Vector

**Idea:** Save the last k elements, shift the remaining elements right by k positions while iterating backward, and copy the saved values to the front.

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

**Example:** [1, 2, 3, 4, 5], k = 2 → [4, 5, 1, 2, 3]

- **Time:** O(n)
- **Extra space:** O(k)

**Common mistake:** When shifting values to the right, iterate from the end toward the beginning so values are not overwritten before being copied.

## 9. Right Rotate by k — Reversal Algorithm

**Idea:** Reverse the whole array, reverse the first k elements, then reverse the remaining elements.

~~~cpp
void reverseRange(vector<int>& nums, int left, int right) {
    while (left < right) {
        swap(nums[left], nums[right]);
        left++;
        right--;
    }
}

void rightRotate(vector<int>& nums, int k) {
    int n = static_cast<int>(nums.size());
    if (n == 0) return;

    k %= n;

    reverseRange(nums, 0, n - 1);
    reverseRange(nums, 0, k - 1);
    reverseRange(nums, k, n - 1);
}
~~~

**Dry run:** [1, 2, 3, 4, 5], k = 2

1. Reverse all → [5, 4, 3, 2, 1]
2. Reverse first two → [4, 5, 3, 2, 1]
3. Reverse the rest → [4, 5, 1, 2, 3]

- **Time:** O(n)
- **Extra space:** O(1)

## 10. Left Rotate by k — Reversal Algorithm

**Idea:** Reverse the first k elements, reverse the remaining elements, then reverse the entire array.

~~~cpp
void reverseRange(vector<int>& nums, int left, int right) {
    while (left < right) {
        swap(nums[left], nums[right]);
        left++;
        right--;
    }
}

void leftRotate(vector<int>& nums, int k) {
    int n = static_cast<int>(nums.size());
    if (n == 0) return;

    k %= n;

    reverseRange(nums, 0, k - 1);
    reverseRange(nums, k, n - 1);
    reverseRange(nums, 0, n - 1);
}
~~~

**Dry run:** [1, 2, 3, 4, 5], k = 2

1. Reverse first two → [2, 1, 3, 4, 5]
2. Reverse the remaining elements → [2, 1, 5, 4, 3]
3. Reverse all → [3, 4, 5, 1, 2]

Another example: [10, 20, 30, 40, 50, 60], k = 3 → [40, 50, 60, 10, 20, 30].

- **Time:** O(n)
- **Extra space:** O(1)

**Common mistakes:** Check n != 0 before k %= n; the second reversal starts at index k, not k + 1; and the order of operations differs from right rotation.

---

## Rotation summary

| Operation | Reversal order | Extra space |
|---|---|---:|
| Left rotate by k | Reverse first k → reverse rest → reverse all | O(1) |
| Right rotate by k | Reverse all → reverse first k → reverse rest | O(1) |
| Left/right rotate with temporary vector | Save moved section, shift, copy back | O(k) |

## General lessons from Array Level 2

1. **Two pointers** help reverse arrays and process elements in place.
2. **Read and write positions** help remove duplicates and move zeroes without another full array.
3. **Preserve order** when a problem requires stable movement of elements.
4. **Handle edge cases:** empty arrays, one element, k = 0, k >= n, and repeated values.
5. **Use modulo safely:** check n == 0 before k %= n.
6. **Know the trade-off:** a temporary vector is straightforward but uses extra space; reversal achieves O(1) extra space.
