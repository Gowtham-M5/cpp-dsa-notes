# LeetCode 1480: Running Sum of 1D Array

**Difficulty:** Easy  
**Topic:** Arrays  
**Language:** C++

## 1. Problem Statement

Given an array `nums`, calculate the running sum of its elements.

The running sum at index `i` is the sum of all elements from index `0` to index `i`.

**Formula:** `runningSum[i] = nums[0] + nums[1] + ... + nums[i]`

### Example

**Input:** `nums = [1, 2, 3, 4]`  
**Output:** `[1, 3, 6, 10]`

**Explanation:**
- Index 0: `1`
- Index 1: `1 + 2 = 3`
- Index 2: `1 + 2 + 3 = 6`
- Index 3: `1 + 2 + 3 + 4 = 10`

## 2. Approach

1. Initialize a variable `sum = 0`.
2. Traverse the array using a `for` loop.
3. Add the current element to `sum`.
4. Store the running sum in the current array position.
5. Return the modified array.

## 3. C++ Solution

```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int sum = 0;

        for (int i = 0; i < nums.size(); i++) {
            sum = sum + nums[i];
            nums[i] = sum;
        }

        return nums;
    }
};
```

## 4. Code Explanation

### A. Initialize the sum
```cpp
int sum = 0;
```
Creates an integer variable to store the running total.

### B. Traverse the array
```cpp
for (int i = 0; i < nums.size(); i++)
```
Visits every element, starting at index `0`. Use `i < nums.size()`, not `i <= nums.size()`, because array indices start at `0`.

### C. Calculate the running sum
```cpp
sum = sum + nums[i];
```
Adds the current element to the previous running total.

### D. Update the current element
```cpp
nums[i] = sum;
```
Replaces the current element with its running sum.

For example, when `i = 1`:
- Previous running sum = `1`
- Current element = `2`
- New running sum = `1 + 2 = 3`
- `nums[1]` becomes `3`

### E. Return the array
```cpp
return nums;
```
The function returns the modified vector containing all running sums. Its return type is `vector<int>`, so it must return a vector, not an integer.

## 5. Dry Run

Input: `[1, 2, 3, 4]`

| Iteration | `nums[i]` before update | `sum` after addition | Array after update |
| --- | --- | --- | --- |
| 1 | 1 | 1 | `[1, 2, 3, 4]` |
| 2 | 2 | 3 | `[1, 3, 3, 4]` |
| 3 | 3 | 6 | `[1, 3, 6, 4]` |
| 4 | 4 | 10 | `[1, 3, 6, 10]` |

Final output: `[1, 3, 6, 10]`

## 6. Important Concepts Learned

- Array traversal using a `for` loop.
- Accessing elements using their indices.
- Maintaining a running total using a variable.
- Updating array elements.
- Understanding function return types.
- Placing `return` after the loop when all iterations must finish.

## 7. Common Mistakes

**Mistake 1: Incorrect loop condition**

Incorrect: `i <= nums.size()`  
Correct: `i < nums.size()`

**Mistake 2: Returning an integer**

```cpp
return sum;
```
Incorrect because the function must return `vector<int>`.

**Mistake 3: Returning inside the loop**

Returning inside the loop ends the function before all elements are processed.

**Mistake 4: Using an unnecessary second array**

The input vector can be updated directly, so a separate result vector is unnecessary for this approach.

## 8. Time and Space Complexity

**Time Complexity: `O(n)`** — the loop visits each element once.  
**Auxiliary Space Complexity: `O(1)`** — the algorithm uses one additional integer variable, `sum`, and modifies the input vector directly.

## 9. Interview Takeaway

A running sum stores the cumulative total as you traverse an array.

```cpp
sum = sum + nums[i];
nums[i] = sum;
```

This pattern is useful for cumulative calculations and is a foundation for learning prefix sums.

**Revision reminder:** Revisit this problem after learning the basics of C++ STL and vectors. Revise the logic once without looking at the solution. Focus on understanding how `sum` changes during each iteration.
