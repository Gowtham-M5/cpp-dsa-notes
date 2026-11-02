# 462. Minimum Moves to Equal Array Elements II

- **LeetCode:** [462. Minimum Moves to Equal Array Elements II](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/)
- **Difficulty:** Medium
- **Topic:** Array, Sorting, Math
- **Status:** Solved — submission accepted (user confirmed on 2026-11-02)
- **Date practiced:** 2026-11-02
- **Pattern:** Sorting + Median + Absolute Difference
- **Language:** C++

---

## 1. Problem Understanding

We are given an integer array. In one move, we can increase or decrease one element by 1.

The goal is to make every element equal using the minimum total number of moves.

If we choose a target value, the moves required for an element are its absolute difference from that target:

`moves = |nums[i] - target|`

So, we need to choose a target that minimizes the sum of absolute differences across all elements.

## 2. Important Concept: Why Median, Not Average?

My first attempt calculated the average of the array and used it as the target. That does not always minimize the total number of moves.

For this problem, a **median** of the array is an optimal target.

The median is the middle value after sorting the array.

### Example

Input:

```text
nums = [1, 0, 0, 8, 6]
```

After sorting:

```text
[0, 0, 1, 6, 8]
```

- Average = (1 + 0 + 0 + 8 + 6) / 5 = 3
- Median = 1

Using the average as the target gives:

```text
|1 - 3| + |0 - 3| + |0 - 3| + |8 - 3| + |6 - 3|
= 2 + 3 + 3 + 5 + 3
= 16
```

Using the median as the target gives:

```text
|1 - 1| + |0 - 1| + |0 - 1| + |8 - 1| + |6 - 1|
= 0 + 1 + 1 + 7 + 5
= 14
```

Therefore, the minimum number of moves is **14**.

### Why does the median work?

After sorting, values smaller than the median are on its left and values greater than the median are on its right. Moving the target away from the median makes the total distance increase or stay the same; choosing a median gives a minimum sum of absolute differences.

For an even-sized array, either of the two middle values is a valid median for this problem.

## 3. Approach Used: Sorting + Median

The solution has three main steps.

### Step 1 — Get the array size and initialize the answer

```cpp
int n = nums.size();
long long count = 0;
```

- `n` stores the number of elements.
- `count` accumulates the total moves.
- We use `long long` because the total can exceed the maximum value of a 32-bit `int`.

### Step 2 — Sort the array

```cpp
sort(nums.begin(), nums.end());
```

Sorting places the elements in ascending order, which makes it possible to select the median by its index.

### Step 3 — Select the median

```cpp
int target = nums[n / 2];
```

C++ uses zero-based indexing.

- If `n = 5`, then `n / 2 = 2`; the middle element is at index 2.
- If `n = 6`, then `n / 2 = 3`; index 3 is one of the two middle positions.

Integer division is used, so this single statement works for both odd and even array sizes.

### Step 4 — Calculate the moves

Traverse every element and add its distance from the target:

```cpp
if(nums[i] > target) {
    count = count + nums[i] - target;
}
else if(nums[i] < target) {
    count = count + target - nums[i];
}
```

If an element is greater than the target, subtract the target from it. If it is smaller, subtract the element from the target. If it equals the target, no moves are needed.

This is equivalent to adding the absolute difference:

`count += abs(nums[i] - target);`

The original if/else approach is kept in my accepted code.

## 4. My Accepted C++ Solution

The following is my final accepted code. It preserves the approach I implemented.

```cpp
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        int n=nums.size();
        long long count=0;
        sort(nums.begin(),nums.end());
        int target;
        
            target=nums[n/2];
    
        for(int i=0;i<nums.size();i++){
            if(nums[i]>target){
                count=count+nums[i]-target;
            }
            else if(nums[i]<target){
                count=count+target-nums[i];
            }
        }
        return count;
    }
};
```

## 5. Dry Run

Input:

```text
nums = [1, 0, 0, 8, 6]
```

### After sorting

```text
[0, 0, 1, 6, 8]
```

Array size:

`n = 5`

Median index:

`n / 2 = 5 / 2 = 2`

Target:

`nums[2] = 1`

### Calculate moves

| Element | Target | Moves required | Running count |
|---:|---:|---:|---:|
| 0 | 1 | 1 | 1 |
| 0 | 1 | 1 | 2 |
| 1 | 1 | 0 | 2 |
| 6 | 1 | 5 | 7 |
| 8 | 1 | 7 | 14 |

Final result:

```text
14
```

## 6. Important C++ Concept: Integer Overflow

My first version used:

```cpp
int count = 0;
```

Some test cases caused signed integer overflow because the accumulated number of moves exceeded the maximum value that a typical 32-bit `int` can store.

The runtime error showed an addition that could not be represented as an `int`.

Correction:

```cpp
long long count = 0;
```

- `int` is typically a 32-bit signed integer.
- `long long` is typically a 64-bit signed integer.
- Use a sufficiently large type for an accumulated result when its maximum can exceed the `int` range.

The function returns `int` because that is the required LeetCode signature, and the problem guarantees that the final answer fits in a 32-bit signed integer.

## 7. Mistakes and Corrections During Practice

| Attempt / issue | What went wrong | Correction / learning |
|---|---|---|
| Used average as target | Average does not always minimize the sum of absolute differences | Use the median |
| Wrote `nums[(n/2)+1]` for odd size | Selected the element after the middle because indexing starts at 0 | Use `nums[n/2]` |
| Wrote `nums.start()` | Incorrect vector iterator function | Use `nums.begin()` |
| Used `int count` | Total moves overflowed the `int` range | Use `long long count` |

## 8. Complexity Analysis

Let `n` be the number of elements.

- **Time Complexity: O(n log n)** — sorting takes O(n log n), and the traversal to calculate moves takes O(n). Sorting dominates.
- **Auxiliary Space: O(1)** excluding the space used internally by the sorting implementation. The code does not create another array.

## 9. Pattern Tracker Note: Sorting + Median

### Core idea

Sort the values, select a median, and calculate the sum of absolute differences from that median.

### When may this pattern be useful?

Look for this idea when a problem asks you to:

- Make all values equal.
- Minimize the total number of increment/decrement operations.
- Minimize the sum of absolute differences from a chosen target.

### Concepts involved

- Sorting an array.
- Zero-based indexing.
- Odd and even array sizes.
- Median selection.
- Absolute difference.
- Accumulation using `long long`.

### Understanding level

I implemented the median-based approach after receiving hints and corrections. I understood why the average was not optimal, how to select the median, and how to avoid integer overflow. Independent application of this pattern still needs further practice; this problem alone does not establish mastery.

## 10. Quick Revision

| Question | Answer |
|---|---|
| What is the optimal target? | A median of the array |
| Why not the average? | It does not always minimize the sum of absolute differences |
| How do we sort a vector? | `sort(nums.begin(), nums.end())` |
| How do we select a median? | `nums[n/2]` after sorting |
| Does `nums[n/2]` work for even sizes? | Yes; it selects one of the two middle elements |
| What does `count` store? | Total moves needed to make all elements equal |
| Why use `long long`? | To prevent overflow while accumulating moves |
| Time complexity | O(n log n) |
| Auxiliary space | O(1), excluding sorting implementation details |
| Submission status | Accepted — 2026-11-02 |

**Core idea:** Sort the array, choose its median as the target, and add the absolute difference between every element and that target.
