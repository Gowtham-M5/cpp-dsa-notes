# Count Digits

**Status:** Concept and coding practice completed

## 1. What Is Count Digits?

Count Digits means finding the total number of digits present in a given non-negative integer.

| Number | Number of digits |
|---:|---:|
| 7 | 1 |
| 42 | 2 |
| 583 | 3 |
| 4062 | 4 |
| 90000 | 5 |
| 0 | 1 |

## 2. Why Do We Need It?

Counting digits is a fundamental number-manipulation problem. It helps us practise loops and mathematical operations on numbers. The same digit-processing technique is useful in:
- Sum of Digits
- Reverse a Number
- Palindrome Number
- Armstrong Number

## 3. Core Intuition

We reuse the digit-extraction technique:

- `n % 10` extracts the last digit.
- `n / 10` removes the last digit (integer division).
- Each time we process one digit, increase a counter by one.

We repeat this until `n` becomes zero.

## 4. C++ Implementation

This is the function-based solution we wrote and corrected during practice:

```cpp
int countDigits(int n) {
    int digit;
    int count = 0;

    if (n == 0) {
        count++;
    }

    while (n > 0) {
        digit = n % 10;
        n = n / 10;
        count++;
    }

    return count;
}
```

**Code explanation:**

1. `count` starts at `0` because no digits have been processed yet.
2. If `n == 0`, increase `count` to `1`. This handles the special case where the input itself is zero.
3. The loop runs while `n > 0`.
4. `n % 10` extracts the last digit and stores it in `digit`.
5. `n / 10` removes the last digit.
6. `count++` increases the count for the digit that was processed.
7. Return `count` after all digits have been processed.

The `digit` variable is not needed to calculate the count itself; it is included here because this is the version we practised using the digit-extraction pattern.

## 5. Examples

**Example 1**

Input: `n = 583`  
Output: `3`

**Example 2**

Input: `n = 90000`  
Output: `5`

Zeros inside a number are counted normally. Every loop iteration represents one digit, including an internal zero.

**Example 3**

Input: `n = 0`  
Output: `1`

Zero itself is a one-digit number.

## 6. Dry Run

For `n = 583`:

| Iteration | `n` before processing | `n % 10` (`digit`) | `n / 10` (updated `n`) | `count` |
|---|---:|---:|---:|---:|
| Initial | 583 | — | — | 0 |
| 1 | 583 | 3 | 58 | 1 |
| 2 | 58 | 8 | 5 | 2 |
| 3 | 5 | 5 | 0 | 3 |

Now `n` is `0`, so `n > 0` is false and the loop stops. The function returns **3**.

### Dry Run for Zero

For `n = 0`:

1. `n == 0` is true.
2. `count++` changes `count` from `0` to `1`.
3. The `while(n > 0)` loop does not execute.
4. The function returns **1**.

## 7. Important Edge Case: Zero

There are two different situations to remember:

- **The input itself is zero:** `n = 0`. The loop does not run, so handle this case separately.
- **The number contains an internal zero:** `n = 10005`. The loop processes every digit, including the zero, so the answer is `5`.

Do not confuse an input of zero with a zero digit inside a number.

## 8. Time Complexity

Let `d` be the number of digits. Each iteration removes exactly one digit.

**Time Complexity: `O(d)`**

## 9. Space Complexity

Only a fixed number of integer variables are used. No extra array or data structure is needed.

**Auxiliary Space Complexity: `O(1)`**

## 10. Common Mistakes

1. **Confusing `%` and `/`:** `n % 10` extracts the last digit; `n / 10` removes it.
2. **Forgetting to update `n`:** without `n = n / 10`, the loop can run forever.
3. **Forgetting the zero edge case:** `while(n > 0)` does not execute when `n == 0`, but the answer should be `1`.
4. **Using assignment instead of comparison:** `n = 0` assigns zero; `n == 0` checks whether the value is zero.
5. **Thinking internal zeros need special handling:** they are counted by the loop like every other digit.

## 11. Practice Problems

1. Count the digits in `7284`.
2. Count the digits in `10005`.
3. Count the digits in `90000`.
4. Explain why the loop does not execute for `n = 0`.
5. Dry-run the function for `n = 4062`.

## 12. Interview Patterns

Count Digits builds on digit extraction and prepares us for:
- **Sum of Digits:** add each extracted digit instead of increasing a counter.
- **Reverse a Number:** build a new number from the extracted digits.
- **Palindrome Number:** reverse the number and compare it with the original.
- **Armstrong Number:** process each digit and calculate its required power.

## 13. Revision Summary

- `n % 10` extracts the last digit.
- `n / 10` removes the last digit through integer division.
- Increase `count` once for every digit processed.
- Handle `n == 0` separately because the loop does not execute.
- Internal zeros are counted normally.
- Time complexity: `O(d)`, where `d` is the number of digits.
- Auxiliary space complexity: `O(1)`.

### Final Memory Trick

```text
n % 10  → Extract the last digit
n / 10  → Remove the last digit
count++ → Count the processed digit
```
