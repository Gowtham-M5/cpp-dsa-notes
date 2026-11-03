# 3736. Minimum Moves to Equal Array Elements III

- **LeetCode:** [3736. Minimum Moves to Equal Array Elements III](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-iii/)
- **Difficulty:** Easy
- **Topic:** Arrays, Math
- **Status:** Solved — submission accepted (user confirmed on 2026-11-03)
- **Date practiced:** 2026-11-03
- **Pattern:** Maximum Tracking + Running Sum
- **Language:** C++

---

## 1. Problem Understanding

In one move, we can increase one array element by 1. The goal is to make all elements equal using the minimum number of moves.

Since elements can only be increased, the best target is the **maximum element already present**. Choosing a larger target would add unnecessary moves, and choosing a smaller target cannot make every element equal using only increments.

For each element, the number of moves needed is:

`moves = maximum - nums[i]`

The answer is the sum of these differences.

## 2. My Accepted C++ Solution

This is the exact code I submitted and confirmed accepted. It is preserved unchanged.

```cpp
class Solution {
public:
    int minMoves(vector<int>& nums) {
       int max=0;
       int n=nums.size();
       int count =0;
       for(int i=0;i<n;i++){
          if(nums[i]>max){
            max=nums[i];
          }
       }
       for(int i=0;i<n;i++){
        if(nums[i]<max){
            count+=max-nums[i];
        }
       }
     return count ;
    }
};
```

## 3. Approach: Two Array Traversals

### Step 1 — Find the maximum element

```cpp
int max = 0;
for (int i = 0; i < n; i++) {
    if (nums[i] > max) {
        max = nums[i];
    }
}
```

Traverse the array and keep updating `max` whenever a larger element is found. After this loop, `max` stores the target value.

### Step 2 — Calculate the total increments

```cpp
for (int i = 0; i < n; i++) {
    if (nums[i] < max) {
        count += max - nums[i];
    }
}
```

For each element smaller than the maximum, add the difference to `count`. An element already equal to the maximum requires zero moves.

## 4. Dry Run

Input:

```text
nums = [2, 1, 3]
```

**First traversal — find maximum:**

| Element | Current maximum |
|---:|---:|
| 2 | 2 |
| 1 | 2 |
| 3 | 3 |

Target = 3.

**Second traversal — count moves:**

| Element | Target | Moves | Running count |
|---:|---:|---:|---:|
| 2 | 3 | 3 - 2 = 1 | 1 |
| 1 | 3 | 3 - 1 = 2 | 3 |
| 3 | 3 | 0 | 3 |

Final answer = **3**.

## 5. Concepts Learned

- **Maximum element tracking:** Traverse an array and maintain the largest value found so far.
- **Two-pass array traversal:** First pass finds the target; second pass calculates the required work.
- **Running sum / accumulation:** Add each element's required increments to `count`.
- **Direct calculation:** Instead of repeatedly incrementing an element in a `while` loop, calculate the number of increments with subtraction.
- **Why the maximum is the target:** With increment-only operations, every element must reach at least the current maximum. Reaching that maximum minimizes the total increments.

## 6. Complexity Analysis

Let `n` be the number of elements.

- **Time Complexity: O(n)** — one traversal finds the maximum and a second traversal calculates the moves. Two linear passes are still O(n).
- **Auxiliary Space Complexity: O(1)** — only a fixed number of variables are used; no additional data structure is created.

## 7. Earlier Attempt and Correction

My first attempt used sorting, selected the middle element as the target, and repeatedly incremented or decremented elements with `while` loops. That approach was based on the median idea from #462, where both increasing and decreasing are allowed.

For this problem, only increasing is allowed, so the median is not the correct target. The maximum element is the correct target. Repeated one-by-one loops are also unnecessary because the required increments can be calculated directly using `max - nums[i]`.

## 8. Problem Tracker Record

- **Problem:** #3736 — Minimum Moves to Equal Array Elements III
- **Difficulty:** Easy
- **Topic:** Arrays, Math
- **Pattern:** Maximum Tracking + Running Sum
- **Status:** Solved — submission accepted
- **Actual approach:** Two passes: find the maximum, then sum the difference between the maximum and every smaller element.
- **Important learning:** The allowed operation determines the target. Median applies when both incrementing and decrementing are allowed; maximum applies when only incrementing is allowed.
- **Time Complexity:** O(n)
- **Auxiliary Space:** O(1)
- **Completion date:** 2026-11-03

## 9. Pattern Tracker Note

**Pattern:** Maximum Tracking + Running Sum

**Core idea:** Maintain the maximum value in one traversal, then use it as the target while accumulating the required differences in another traversal.

**When it may be useful:** When a problem asks for the largest value, or when every element must be brought up to a common value and the permitted operation is increment-only.

**Problem practiced:** #3736 — Minimum Moves to Equal Array Elements III.

**Understanding demonstrated:** I first attempted a median-and-sorting approach, then corrected the target to the maximum and independently implemented two traversals with direct difference calculation. The submission was accepted.

**Understanding level:** Demonstrated understanding with this problem. Do not mark the pattern as mastered based on one problem; confirm independent application in future practice.
