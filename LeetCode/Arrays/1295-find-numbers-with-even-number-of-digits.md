# LeetCode 1295 — Find Numbers with Even Number of Digits

## Problem
Count how many numbers in the array contain an even number of digits.

## Core idea: Count digits of each number
For each number:
1. Keep its value in a temporary variable so the original array element is unchanged.
2. Repeatedly divide the temporary number by 10.
3. Increase a digit counter each time the loop runs.
4. If the digit count is even, increase the answer.

## Example
For `nums = [12,345,2,6,7896]`:
- `12` has 2 digits — even.
- `345` has 3 digits — odd.
- `2` has 1 digit — odd.
- `6` has 1 digit — odd.
- `7896` has 4 digits — even.

There are 2 numbers with an even number of digits.

## Important details
- `num /= 10` removes the last digit each iteration.
- `digits % 2 == 0` checks whether the digit count is even.
- The problem's constraints use positive integers.

## Code note
The code previously saved here was not verified as the exact code I personally wrote. It has been removed rather than presenting an assistant-written implementation as mine. Add my own code after retrying the problem.

## Complexity
If `n` is the number of array elements and `d` is the maximum number of digits:
- Time: `O(n × d)`
- Extra space: `O(1)`
