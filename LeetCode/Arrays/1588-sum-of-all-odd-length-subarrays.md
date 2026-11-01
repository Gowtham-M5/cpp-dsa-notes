# 1588. Sum of All Odd Length Subarrays

- **LeetCode:** [1588. Sum of All Odd Length Subarrays](https://leetcode.com/problems/sum-of-all-odd-length-subarrays/)
- **Difficulty:** Easy
- **Topic:** Arrays
- **Pattern:** Nested Loops + Subarray Enumeration
- **Status:** Solved — submission accepted
- **Date practiced:** 2026-11-01

## 1. Problem Understanding

Given an integer array, return the sum of all possible **contiguous subarrays whose lengths are odd**.

A subarray is a continuous portion of an array. We must consider every possible starting position for each possible odd length.

Example:

```text
arr = [1, 2, 3, 4, 5]
```

The odd subarray lengths are 1, 3, and 5.

- Length 1: `[1]`, `[2]`, `[3]`, `[4]`, `[5]`
- Length 3: `[1, 2, 3]`, `[2, 3, 4]`, `[3, 4, 5]`
- Length 5: `[1, 2, 3, 4, 5]`

Calculate the sum of each listed subarray, then add those sums together.

## 2. Approach: Three Nested Loops

We enumerate every possible subarray using three loops. Each loop has a separate responsibility.

| Variable | Responsibility |
| --- | --- |
| `i` | Selects the subarray length |
| `j` | Selects the starting index |
| `k` | Traverses the elements in the selected subarray |

### Step 1 — Initialize the final answer

```cpp
int totalsum = 0;
```

This variable accumulates the sum of all valid odd-length subarrays. It is initialized before the loops because it must not reset while processing different subarrays.

### Step 2 — Select each possible subarray length

```cpp
for(int i = 1; i <= arr.size(); i++)
```

Here, `i` represents a **length**, not an array index. For an array of size 5, the possible lengths are 1, 2, 3, 4, and 5.

### Step 3 — Process only odd lengths

```cpp
if(i % 2 != 0)
```

The modulo operator checks whether the selected length is odd.

| i | i % 2 | Result |
| ---: | ---: | --- |
| 1 | 1 | Odd — process |
| 2 | 0 | Even — skip |
| 3 | 1 | Odd — process |
| 4 | 0 | Even — skip |
| 5 | 1 | Odd — process |

### Step 4 — Select every valid starting index

```cpp
for(int j = 0; j <= arr.size() - i; j++)
```

For an array of size `n` and a selected subarray length `i`, the last valid starting index is `n - i`.

Example: if `n = 5` and `i = 3`, the last valid starting index is `5 - 3 = 2`. Therefore, valid starting indices are 0, 1, and 2.

We use `<=` so that the last valid starting index is included. Using only `<` would miss that final subarray.

### Step 5 — Reset the current subarray sum

```cpp
int sum = 0;
```

This is inside the second loop because every new starting index represents a new subarray. Its sum must start from zero.

### Step 6 — Traverse the selected subarray

```cpp
for(int k = j; k < j + i; k++)
```

The third loop starts at `j` and visits exactly `i` elements.

For example, when `j = 1` and `i = 3`, it visits indices 1, 2, and 3.

### Step 7 — Add elements and then add the completed subarray sum

```cpp
sum += arr[k];
```

After the third loop finishes, the complete sum of the selected subarray is available. Add it to the final answer:

```cpp
totalsum += sum;
```

This statement belongs **after** the third loop. If it were inside the third loop, intermediate running sums would be added repeatedly.

## 3. Complete Dry Run and Trace

Input:

```text
arr = [1, 2, 3, 4, 5]
n = 5
totalsum = 0
```

### Case 1: i = 1 — odd length

All single-element subarrays are considered.

| j | Elements visited by k | Subarray | sum | totalsum after addition |
| ---: | --- | --- | ---: | ---: |
| 0 | index 0 | [1] | 1 | 1 |
| 1 | index 1 | [2] | 2 | 3 |
| 2 | index 2 | [3] | 3 | 6 |
| 3 | index 3 | [4] | 4 | 10 |
| 4 | index 4 | [5] | 5 | 15 |

Contribution from length 1 = **15**.

### Case 2: i = 2 — even length

`2 % 2 != 0` is false, so the body of the odd-length condition is skipped.

No subarray is processed. `totalsum` remains **15**.

### Case 3: i = 3 — odd length

The second loop condition is `j <= 5 - 3`, so valid starting indices are 0, 1, and 2.

| j | Elements visited by k | Subarray | sum | totalsum after addition |
| ---: | --- | --- | ---: | ---: |
| 0 | indices 0, 1, 2 | [1, 2, 3] | 1 + 2 + 3 = 6 | 21 |
| 1 | indices 1, 2, 3 | [2, 3, 4] | 2 + 3 + 4 = 9 | 30 |
| 2 | indices 2, 3, 4 | [3, 4, 5] | 3 + 4 + 5 = 12 | 42 |

Contribution from length 3 = **27**. Running total = **42**.

### Case 4: i = 4 — even length

`4 % 2 != 0` is false, so this length is skipped.

`totalsum` remains **42**.

### Case 5: i = 5 — odd length

The second loop condition is `j <= 5 - 5`, so only starting index 0 is valid.

| j | Elements visited by k | Subarray | sum | totalsum after addition |
| ---: | --- | --- | ---: | ---: |
| 0 | indices 0, 1, 2, 3, 4 | [1, 2, 3, 4, 5] | 15 | 57 |

Contribution from length 5 = **15**.

### Final calculation

```text
Length 1 contribution = 15
Length 3 contribution = 27
Length 5 contribution = 15

Final answer = 15 + 27 + 15 = 57
```

Output:

```text
57
```

## 4. Why the Sum Variables Are Initialized at Different Levels

There are two accumulators with different jobs:

- **`totalsum`** is initialized before all loops. It stores the combined answer across every valid subarray and must keep its value throughout the function.
- **`sum`** is initialized inside the second loop, before the third loop. It stores the sum of only the currently selected subarray, so it must reset for every new starting index.

If `sum` were initialized inside the third loop, it would reset for every element and could not accumulate the complete subarray sum.

Similarly, `totalsum += sum` must be after the third loop, so only the completed subarray sum is added once.

## 5. My Accepted C++ Solution

The following is the exact code I submitted and got accepted. It is preserved unchanged.

```cpp
class Solution {
public:
    int sumOddLengthSubarrays(vector<int>& arr) {
        int totalsum=0;

        for(int i=1;i<=arr.size();i++){
            if(i%2 != 0){
                for(int j=0;j<=arr.size()-i;j++){
                    int sum=0;
                    for(int k=j;k<j+i;k++){
                        sum+=arr[k];
                        
                    }
                    totalsum+=sum;
                }
            }

        }
        return totalsum;
    }
};
```

## 6. Complexity Analysis

Let `n` be the number of elements in the array.

- **Time Complexity: O(n³).** The outer loop considers up to `n` lengths. For each length, the second loop considers up to `n` starting positions. For each starting position, the third loop can visit up to `n` elements. Thus, the straightforward upper bound is cubic.
- **Auxiliary Space Complexity: O(1).** Only a fixed number of variables are used: `totalsum`, `sum`, and the loop variables. The input array is not modified and no additional data structure is created.

## 7. Mistakes Corrected During Practice

1. **Using `arr.length`:** C++ vectors use `arr.size()` to get their number of elements.
2. **Outer loop meaning:** The outer loop variable `i` represents the selected subarray length, not an array index.
3. **Odd-length condition:** Check the selected length using `i % 2 != 0`, not the total array size.
4. **Second-loop boundary:** Use `j <= arr.size() - i`. Using `<` misses the final valid starting position.
5. **Resetting the current sum:** Initialize `sum = 0` inside the second loop so each subarray gets a fresh sum.
6. **Adding the completed sum:** Add `sum` to `totalsum` after the third loop, not during each element addition.

## 8. Concepts Learned

- A subarray is a contiguous part of an array.
- The subarray length is the number of elements in that range.
- Modulo (`%`) can be used to check odd and even values.
- Nested loops can have different responsibilities.
- The last valid starting index for a subarray of length `len` in an array of size `n` is `n - len`.
- The condition `j <= n - len` includes the last valid starting index.
- An accumulator must be initialized at the level where it needs to reset.
- Add the completed subarray sum once, after traversing its elements.

## 9. Pattern Tracker Note

**Pattern:** Nested Loops — Subarray Enumeration

**Core idea:** Choose a subarray length, visit every valid starting position for that length, and traverse the selected range to process its elements.

**When it may be useful:** When a problem asks us to examine every contiguous subarray and the input constraints allow straightforward enumeration.

**Problem practiced:** #1588 — Sum of All Odd Length Subarrays.

**Understanding demonstrated:** I explained that we should process odd lengths, move the starting index through valid positions, and traverse the selected range to calculate its sum. With hints, I mapped the outer loop to the subarray length, derived the inclusive starting-index boundary, and identified where the current sum must reset.

**Next learning point:** Practise deriving loop boundaries and accumulator initialization independently in another subarray problem. This one problem is not enough to mark the pattern as mastered.
