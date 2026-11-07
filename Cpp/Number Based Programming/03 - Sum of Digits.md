# Sum of Digits

**Status:** Concept and coding practice completed

## 1. What Is Sum of Digits?

Sum of Digits means adding all the individual digits of a given non-negative integer.

| Number | Sum of its digits |
|---:|---:|
| 1234 | 10 |
| 456 | 15 |
| 9005 | 14 |
| 0 | 0 |

## 2. Why Do We Need It?

Sum of Digits is a basic number-manipulation problem. It helps us practise loops, digit extraction, integer division, and accumulating a result.

The same digit-processing pattern is useful in:
- Reverse a Number
- Palindrome Number
- Armstrong Number

## 3. Core Intuition

We use the digit-extraction technique:

- `n % 10` extracts the last digit.
- Add that digit to `sum`.
- `n / 10` removes the last digit through integer division.
- Repeat until `n` becomes zero.

We use a `while` loop because we do not know in advance how many digits the number contains.

## 4. C++ Implementation

This is the function-based solution we wrote and practised:

```cpp
int sumofDigits(int n) {
    int digit;
    int sum = 0;

    if (n == 0) {
        return 0;
    }

    while (n > 0) {
        digit = n % 10;
        n = n / 10;
        sum += digit;
    }

    return sum;
}
```

**Code explanation:**

1. `digit` stores the last digit extracted from the number.
2. `sum` starts at `0` because no digits have been added yet.
3. If `n == 0`, return `0`. This handles zero directly.
4. The `while (n > 0)` loop processes the digits one by one.
5. `digit = n % 10` extracts the last digit.
6. `n = n / 10` removes the last digit.
7. `sum += digit` adds the extracted digit to the running total.
8. After all digits are processed, return `sum`.

**Small code improvement:** The explicit `if (n == 0)` check is optional for this implementation. If `n` is zero, the loop does not execute and the function naturally returns the initial value of `sum`, which is also zero.

## 5. Examples

**Example 1**

Input: `n = 1234`  
Calculation: `1 + 2 + 3 + 4 = 10`  
Output: `10`

**Example 2**

Input: `n = 9005`  
Calculation: `9 + 0 + 0 + 5 = 14`  
Output: `14`

**Example 3**

Input: `n = 0`  
Output: `0`

Zeros inside a number contribute zero to the sum, but they are still processed as digits.

## 6. Dry Run

For `n = 1234`:

| Iteration | `n` before processing | `n % 10` (`digit`) | `n / 10` (updated `n`) | `sum` after addition |
|---|---:|---:|---:|---:|
| Initial | 1234 | — | — | 0 |
| 1 | 1234 | 4 | 123 | 4 |
| 2 | 123 | 3 | 12 | 7 |
| 3 | 12 | 2 | 1 | 9 |
| 4 | 1 | 1 | 0 | 10 |

Now `n` is `0`, so the loop stops. The function returns **10**.

## 7. Important Edge Cases

- **Input is zero:** `n = 0`. The loop does not execute and the function returns `0`.
- **Number contains internal zeros:** `n = 9005`. Every digit is processed; adding the zero digits does not change the sum.
- **Positive single-digit number:** `n = 7`. The function returns `7`.

This implementation assumes a non-negative integer, matching the problems practised so far. Negative inputs would need an explicit decision about how to handle the sign.

## 8. Time Complexity

Let `d` be the number of digits in `n`. Each loop iteration removes exactly one digit.

**Time Complexity: `O(d)`**, which is also written as `O(log₁₀ n)` for positive `n`.

## 9. Space Complexity

Only a fixed number of integer variables are used. No extra array or data structure is needed.

**Auxiliary Space Complexity: `O(1)`**

## 10. Common Mistakes

1. **Confusing `%` and `/`:** `n % 10` extracts the last digit; `n / 10` removes it.
2. **Forgetting to update `n`:** without `n = n / 10`, the loop can run forever.
3. **Not initializing `sum`:** the accumulator must start at `0`.
4. **Adding the wrong value:** add `digit` to `sum`, not the whole number `n`.
5. **Using assignment instead of comparison:** `n = 0` assigns zero; `n == 0` checks whether the value is zero.
6. **Unnecessary variables:** a counter is not needed because we are calculating a sum, not counting digits.

## 11. Practice Problems

1. Find the sum of digits of `456`.
2. Find the sum of digits of `9005`.
3. Find the sum of digits of `70001`.
4. What does the function return for `n = 0`?
5. Dry-run the function for `n = 582`.

## 12. Interview Patterns

Sum of Digits builds on digit extraction:
- **Count Digits:** count each processed digit instead of adding it.
- **Reverse a Number:** build a new number from extracted digits.
- **Palindrome Number:** reverse the number and compare it with the original.
- **Armstrong Number:** process each digit and calculate its required power.

## 13. Revision Summary

- `n % 10` extracts the last digit.
- `n / 10` removes the last digit through integer division.
- `sum += digit` adds each extracted digit to the running total.
- Initialize `sum = 0`.
- The loop stops when `n` becomes zero.
- Time complexity: `O(d)`, where `d` is the number of digits.
- Auxiliary space complexity: `O(1)`.

### Final Memory Trick

```text
n % 10     → Extract the last digit
n / 10     → Remove the last digit
sum += digit → Add the digit to the running sum
```
