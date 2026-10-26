# LeetCode 1295 — Find Numbers with Even Number of Digits

## Problem
Count how many numbers in the array contain an even number of digits.

## Core idea: Count digits of each number
For each number, use a temporary variable and repeatedly divide it by 10. Each division removes the last digit. If the digit count is even, increase the answer.

## Code from my practiced solution
```cpp
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int count = 0;
        for (int i = 0; i < nums.size(); i++) {
            int num = nums[i];
            int digits = 0;
            while (num > 0) {
                num /= 10;
                digits++;
            }
            if (digits % 2 == 0) {
                count++;
            }
        }
        return count;
    }
};
```

## Important details
- `num` is a temporary copy, so `nums[i]` stays unchanged.
- `num /= 10` removes the last digit each iteration.
- `digits % 2 == 0` checks whether the digit count is even.
- The problem's constraints use positive integers.

## Example
For `nums = [12,345,2,6,7896]`, the numbers with an even digit count are `12` and `7896`. Answer: `2`.

## Complexity
If `n` is the number of elements and `d` is the maximum number of digits:
- Time: `O(n × d)`
- Extra space: `O(1)`
