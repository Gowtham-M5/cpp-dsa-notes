# LeetCode 1295 — Find Numbers with Even Number of Digits

## Problem
Count how many numbers in the array contain an even number of digits.

## Core idea: Count digits of each number
For each number, repeatedly divide it by 10 and increment a digit counter. If the digit count is even, increment the answer.

## C++ solution
```cpp
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int answer = 0;

        for (int i = 0; i < nums.size(); i++) {
            int num = nums[i];
            int digits = 0;

            while (num > 0) {
                digits++;
                num /= 10;
            }

            if (digits % 2 == 0) {
                answer++;
            }
        }

        return answer;
    }
};
```

## Important details
- Use a temporary variable `num) so the original array value is not changed.
- `num /= 10` removes the last digit each iteration.
- `digits % 2 == 0` checks whether the digit count is even.
- LeetCode's constraints make the input numbers positive.

## Complexity
- Time: `O(n × d)), where `d` is the maximum number of digits.
- Extra space: `O(1)`
