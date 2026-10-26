# LeetCode 1512 — Number of Good Pairs

## Problem
Count pairs of indices `(i, j)` where `nums[i] == nums[j]` and `i < j`.

## Core idea: Compare each pair once
Use nested loops:
- `i` selects an element.
- `j` starts at `i + 1), so only later elements are checked.
- If `nums[i] == nums[j]`, increase the pair count.

Starting `j` at `i + 1` avoids comparing an element with itself and prevents counting the same pair twice.

## Example
Input: `[1,2,3,1,1,3]`

Matching index pairs:
- `(0,3)`
- `(0,4)`
- `(2,5)`
- `(3,4)`

Output: `4`.

## Code note
The code previously saved here was not verified as the exact code I personally wrote. It has been removed rather than presenting an assistant-written implementation as mine. Add my own code after retrying the problem.

## Complexity
- Time: `O(n^2))
- Extra space: `O(1)`
