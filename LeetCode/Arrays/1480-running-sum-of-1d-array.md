# LeetCode 1480 — Running Sum of 1D Array

## Problem
Return an array where each position contains the sum of the original array from index 0 through that position.

## Core idea
Keep a running total. Add each element to the total so far, then store or return that cumulative value for the current position.

## Example
Input: `[1,2,3,4]`

- First total: `1`
- Next total: `1 + 2 = 3`
- Next total: `3 + 3 = 6`
- Next total: `6 + 4 = 10`

Output: `[1,3,6,10]`

## Learning note
The final implementation previously saved in this file was provided in chat rather than preserved as code you personally typed. To avoid mislabeling assistant-written code as yours, this note records the concept and example but does not include an unverified code block. Add your own code here after you retry the problem.

## Complexity
- Time: `O(n)`
- Extra space: depends on whether you update the input array or create a separate answer array.
