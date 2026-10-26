# LeetCode 1480 — Running Sum of 1D Array

## Problem
Return an array where each position contains the sum of the original array from index 0 through that position.

## Core idea
Keep a running total. Add the current element to the total, then store that cumulative value in the answer at the current index.

## Example
Input: `[1,2,3,4]`

- First total: `1`
- Next total: `1 + 2 = 3`
- Next total: `3 + 3 = 6`
- Next total: `6 + 4 = 10`

Output: `[1,3,6,10]`

## Code note
I don't have a reliable record of the exact code you personally typed for this problem. Since you asked me not to put assistant-written code in your notes as if it were yours, I have left the code section out for now. When you retry it and send your code, I'll add your version.

## Complexity
- Time: `O(n)`
- Extra space: `O(n)` if you create a separate answer vector; `O(1)` extra space if you update `nums` in place.
