# LeetCode #724: Find Pivot Index

**Date Practiced:** 27 October 2026  
**Difficulty:** Easy  
**Topic:** Arrays  
**Pattern:** Total Sum + Running Left Sum  
**Status:** Solved — Submission Accepted

## 1. Problem Statement

Given an integer array `nums`, find the pivot index.

A pivot index is an index where the sum of all elements strictly to its left equals the sum of all elements strictly to its right.

- The pivot element is excluded from both sums.
- If multiple pivot indices exist, return the leftmost one.
- If no pivot index exists, return `-1`.

**LeetCode:** [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index/)

## 2. My Approach

I used the total sum of the array and a running left sum to calculate the right sum without traversing the right side separately.

### Step 1: Calculate the total sum

Initialize `totalsum = 0` and traverse the array. Add every element to `totalsum`.

### Step 2: Calculate the right sum

For each index, calculate:

```cpp
rightsum = totalsum - leftsum - nums[i];
```

Here:
- `totalsum` is the sum of the entire array.
- `leftsum` is the sum of elements before the current index.
- `nums[i]` is the current element.

Subtracting the left sum and current element from the total gives the right sum.

### Step 3: Check for the pivot index

If `leftsum == rightsum`, return the current index `i`.

### Step 4: Update the left sum

If the current index is not the pivot, add its element to `leftsum`:

```cpp
leftsum += nums[i];
```

Then move to the next index.

**Important:** Check the pivot condition before updating `leftsum`. The current element must not be included in either the left sum or the right sum.

### Step 5: Return -1

If the loop finishes without finding a pivot index, return `-1`.

## 3. My Accepted Code

```cpp
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
         
     int rightsum=0;
     int leftsum=0;
     int totalsum=0;
     for (int i=0;i<nums.size();i++){
        totalsum=totalsum+nums[i];
     }
     for(int i=0;i<nums.size();i++){
        rightsum=totalsum-leftsum-nums[i];
        if(leftsum==rightsum){
            return i;
        }
        leftsum +=nums[i];
     }
return -1;
    }
};
```

## 4. Example and Dry Run

**Input:** `nums = [1, 7, 3, 6, 5, 6]`

First, calculate the total sum:

`totalsum = 1 + 7 + 3 + 6 + 5 + 6 = 28`

Initially, `leftsum = 0`.

| Index | nums[i] | Left Sum | Right Sum | Pivot? |
|---:|---:|---:|---:|---|
| 0 | 1 | 0 | 27 | No |
| 1 | 7 | 1 | 20 | No |
| 2 | 3 | 8 | 17 | No |
| 3 | 6 | 11 | 11 | Yes |

At index `3`:

- **Left sum:** `1 + 7 + 3 = 11`
- **Right sum:** `5 + 6 = 11`

Since both sums are equal, the function returns `3`.

**Output:** `3`

## 5. Important Concepts Learned

### A. Total Sum

Calculate the sum of all array elements in one traversal.

### B. Running Left Sum

Maintain the sum of elements before the current index. Update it as you move through the array.

### C. Calculate the Right Sum

Instead of using another loop to calculate the right sum for every index, use:

`rightsum = totalsum - leftsum - nums[i]`

This avoids repeated calculations.

### D. Order of Operations

The order in the code is:

1. Calculate `rightsum`.
2. Compare `leftsum` and `rightsum`.
3. Return the index if they are equal.
4. Otherwise, update `leftsum`.

This ensures that the current element is excluded from both sums.

## 6. Time and Space Complexity

- **Time Complexity: `O(n)`** — the code traverses the array twice.
- **Auxiliary Space Complexity: `O(1)`** — only a fixed number of variables are used.

## 7. Pattern Tracker Notes

**Pattern:** Total Sum + Running Left Sum

**Core idea:** Calculate the total sum once, maintain the left sum as the index moves, and derive the right sum from the total.

**When to recognize this pattern:** Look for problems that ask you to compare sums on the left and right of each index or find an index that divides an array into equal-sum parts.

**Problem practiced:** #724 — Find Pivot Index

**Concepts used:** Array traversal, running sum, total sum, arithmetic, conditional statements, and returning an index.

**Understanding level:** Demonstrated through an accepted solution; independent mastery has not yet been assessed.

## 8. Final Takeaway

`Right Sum = Total Sum - Left Sum - Current Element`

By maintaining the left sum and calculating the right sum from the total, we can find the pivot index in linear time without nested loops.
