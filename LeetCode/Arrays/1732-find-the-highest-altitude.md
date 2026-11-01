# 1732. Find the Highest Altitude

- **LeetCode:** [1732. Find the Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude/)
- **Difficulty:** Easy
- **Topic:** Array
- **Status:** Solved — submission accepted
- **Pattern:** Running Sum (Prefix Sum) + Maximum Tracking
- **Language:** C++

---

## 1. Problem Understanding

A biker starts the journey at altitude **0**. The array `gain` tells us how much the altitude changes after each point.

- A positive value increases the altitude.
- A negative value decreases the altitude.
- A zero value keeps the altitude unchanged.

We need to return the **highest altitude reached**, including the starting altitude of 0.

### Example

```text
Input: gain = [-5, 1, 5, 0, -7]
Output: 1
```

The altitudes reached are:

```text
Starting altitude = 0
After -5          = -5
After +1          = -4
After +5          =  1
After  0          =  1
After -7          = -6

Highest altitude = 1
```

---

## 2. Approach Used

We use two variables:

| Variable | Purpose |
|---|---|
| `global` | Stores the current altitude (running sum). |
| `highest` | Stores the highest altitude found so far. |

Both variables start at 0 because the biker begins at altitude 0.

### Steps

1. Initialize `global = 0` to represent the current altitude.
2. Initialize `highest = 0` to include the starting altitude as a possible maximum.
3. Traverse the `gain` array from left to right.
4. Save the current gain value in `cur`.
5. Add `cur` to `global` to calculate the new altitude.
6. Compare the new altitude with `highest` and update `highest` if needed.
7. After processing every element, return `highest`.

### Why do we use `cur`?

`cur` temporarily stores the current gain value:

```cpp
int cur = gain[i];
global = global + cur;
```

This makes the current gain clear and lets us use it to update the running altitude. The input array is not modified.

### Why does this work?

Each element in `gain` represents the change from the previous altitude. Therefore, adding the values one by one gives the altitude at every point.

We do not need to store all the altitudes. We only need:
- the current altitude to calculate the next one;
- the maximum altitude seen so far.

This allows us to solve the problem in one traversal using constant extra space.

---

## 3. My Accepted C++ Solution

```cpp
class Solution {
public:
    int largestAltitude(vector<int>& gain) {
        int global=0;
        int highest = 0;
        for(int i=0;i<gain.size();i++){
            int cur=gain[i];
            
            global=global+cur;
            highest=max(global,highest);

        }
        return highest;
    }
};
```

---

## 4. Code Explanation

### `int global = 0;`

- Stores the current altitude.
- It is updated by adding each gain value.
- It acts as a running sum (prefix sum).

### `int highest = 0;`

- Stores the maximum altitude reached so far.
- It starts at 0 because the starting altitude itself must be considered.
- This is important when all the gain values are negative: the answer should still be 0.

### `for (int i = 0; i < gain.size(); i++)`

- Traverses every element in the array.
- The condition uses `i < gain.size()`, so the last valid index is `gain.size() - 1`.

### `int cur = gain[i];`

- Stores the current gain value in a temporary variable.

### `global = global + cur;`

- Adds the current gain to the previous altitude.
- The updated `global` is the altitude after this point.

The code only reads from `gain`; it does not modify the input array.

### `highest = max(global, highest);`

- Compares the current altitude with the maximum altitude recorded so far.
- Keeps whichever value is greater.

### `return highest;`

- Returns the highest altitude found during the journey.

---

## 5. Dry Run

Input:

```text
gain = [-5, 1, 5, 0, -7]
```

Initial values:

```text
global = 0
highest = 0
```

| Index | `cur` (current gain) | Calculation | Current altitude (`global`) | Highest |
|---:|---:|---|---:|---:|
| Start | — | Initial altitude | 0 | 0 |
| 0 | -5 | 0 + (-5) | -5 | 0 |
| 1 | 1 | -5 + 1 | -4 | 0 |
| 2 | 5 | -4 + 5 | 1 | 1 |
| 3 | 0 | 1 + 0 | 1 | 1 |
| 4 | -7 | 1 + (-7) | -6 | 1 |

Final result:

```text
return 1
```

---

## 6. Pattern Learned: Running Sum + Maximum Tracking

### Running Sum

A running sum maintains the accumulated result while traversing an array.

In this problem:

```cpp
global = global + gain[i];
```

The variable `global` keeps the current altitude by accumulating all gain values processed so far.

### Maximum Tracking

Maximum tracking means maintaining the largest value encountered during traversal.

In this problem:

```cpp
highest = max(global, highest);
```

After every altitude update, we compare the current altitude with the maximum found so far.

### When can this pattern be useful?

Look for this pattern when a problem asks you to:
- calculate cumulative values while traversing an array;
- find the maximum or minimum among intermediate results;
- track the highest or lowest level reached after a sequence of changes;
- process increases and decreases without storing every intermediate result.

### Related concepts

- Array traversal
- Accumulation
- Running sum / prefix sum
- Maximum-so-far tracking
- Handling positive, negative, and zero values

---

## 7. Time and Space Complexity

Let `n` be the number of elements in the `gain` array.

### Time Complexity: O(n)

- The loop visits each array element exactly once.
- Each iteration performs constant-time operations: addition and maximum comparison.
- Therefore, the total time grows linearly with the input size.

### Auxiliary Space Complexity: O(1)

- Only two extra integer variables are used: `global` and `highest`.
- No additional array or data structure is created.
- Therefore, the auxiliary space is constant.

**Final complexity:**
- **Time:** O(n)
- **Auxiliary Space:** O(1)

---

## 8. Important Learning and Mistakes Corrected

During the first attempt, the loop condition was:

```cpp
i <= gain.size()
```

This is incorrect because valid array indices range from `0` to `gain.size() - 1`. Using `<=` attempts to access one position beyond the array.

The corrected condition is:

```cpp
i < gain.size()
```

The accepted solution uses `cur` as a temporary variable to hold the current gain before adding it to the running altitude. It does not overwrite or otherwise modify the input array.

### Key takeaways

1. Check loop boundaries carefully to avoid out-of-bounds access.
2. Initialize the maximum to 0 when the starting altitude is also a valid point.
3. A running sum can represent the current state after each change.
4. Track the maximum during traversal instead of storing every intermediate value.
5. Avoid modifying the input array when the problem does not require it.

---

## 9. Quick Revision

| Question | Answer |
|---|---|
| What does `global` store? | Current altitude / running sum |
| What does `highest` store? | Maximum altitude reached so far |
| Why initialize `highest` to 0? | The starting altitude is 0 and must be considered |
| Which pattern is used? | Running Sum + Maximum Tracking |
| What does `cur` store? | The current gain value from `gain[i]` |
| Does the solution modify the input array? | No |
| Time complexity? | O(n) |
| Auxiliary space complexity? | O(1) |
| Submission status? | Accepted |

**Core idea:** Keep a running altitude, update the highest altitude after every change, and return the maximum.
