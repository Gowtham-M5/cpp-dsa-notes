# 1470. Shuffle the Array

- **LeetCode:** [1470. Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/)
- **Difficulty:** Easy
- **Topic:** Array
- **Status:** Practiced — acceptance not confirmed
- **Pattern:** Array rearrangement using index mapping

## Problem

Given an array `nums` containing `2n` elements in the form `[x1, x2, ..., xn, y1, y2, ..., yn]`, rearrange it into `[x1, y1, x2, y2, ..., xn, yn]`.

## Example

**Input**
```text
nums = [2, 5, 1, 3, 4, 7], n = 3
```

**Output**
```text
[2, 3, 5, 4, 1, 7]
```

## Approach: Use a New Vector and Index Mapping

The input array has two equal halves:

- First half: indexes `0` to `n-1`
- Second half: indexes `n` to `2n-1`

For each index `i` from `0` to `n-1`:

1. Read the element from the first half using `nums[i]`.
2. Read its matching element from the second half using `nums[i+n]`.
3. Append both elements to the result vector in that order.

The expression `i+n` maps an index in the first half to the corresponding position in the second half.

### Index walkthrough

For `nums = [2, 5, 1, 3, 4, 7]` and `n = 3`:

| i | nums[i] | nums[i+n] | Result after this iteration |
|---|---:|---:|---|
| 0 | 2 | 3 | [2, 3] |
| 1 | 5 | 4 | [2, 3, 5, 4] |
| 2 | 1 | 7 | [2, 3, 5, 4, 1, 7] |

## My Practiced C++ Solution

```cpp
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> result;

        for (int i = 0; i < n; i++) {
            result.push_back(nums[i]);
            result.push_back(nums[i + n]);
        }

        return result;
    }
};
```

## Concepts Learned

- **Vector declaration:** `vector<int> result;` creates an initially empty dynamic array of integers.
- **Array traversal:** A `for` loop visits the first-half indexes from `0` through `n-1`.
- **Array indexing:** `nums[i]` accesses an element by its index.
- **Index mapping:** `nums[i+n]` accesses the corresponding element in the second half.
- **Vector `push_back()`:** Appends an element to the end of a vector. Two elements are appended in each loop iteration.
- **Returning a vector:** `return result;` returns the rearranged vector from the function.

## Pattern

**Array rearrangement using index mapping**

Recognize this idea when elements from known positions or sections of an array must be combined in a particular order. Here, each iteration takes one element from each half and appends them alternately to a new vector.

This is not a two-pointers, sorting, or backtracking solution.

## Complexity

Let `n` be the size of each half (the input array has `2n` elements).

- **Time:** `O(n)` — the loop runs `n` times and performs two vector appends per iteration.
- **Auxiliary space:** `O(n)` — the result vector stores `2n` elements.

## Key Takeaway

For two equal halves, the corresponding element in the second half can be found by adding the half-size to the current first-half index: `i + n`.
