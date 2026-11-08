# Reverse a Number

**Status:** Concept and coding practice completed, including negative numbers and integer-overflow handling.

## 1. What Is Reversing a Number?

Reversing a number means arranging its digits in the opposite order.

| Input | Reversed output |
|---:|---:|
| 1234 | 4321 |
| 567 | 765 |
| 1200 | 21 |
| 9876 | 6789 |
| -456 | -654 |
| 0 | 0 |

Leading zeroes in the reversed result are not stored, so reversing `1200` gives `21`.

## 2. Why Do We Need It?

This problem strengthens our understanding of digit extraction, loops, and building a number one digit at a time. It is also a foundation for the Palindrome Number problem.

## 3. Core Intuition

We already know two operations:

- `n % 10` extracts the last digit.
- `n / 10` removes the last digit (integer division).

To build the reversed number, shift the digits already stored one place left by multiplying by 10, then append the newly extracted digit:

```cpp
reverse = reverse * 10 + digit;
```

For example, if `reverse = 43` and `digit = 2`:

```text
reverse = 43 * 10 + 2
        = 432
```

Repeat until the original number becomes zero.

## 4. Basic C++ Implementation (Non-negative Input)

This is the basic version we first developed:

```cpp
int reverseNumber(int n) {
    int digit;
    int reverse = 0;

    if (n == 0) {
        return 0;
    }

    while (n > 0) {
        digit = n % 10;
        reverse = reverse * 10 + digit;
        n = n / 10;
    }

    return reverse;
}
```

This version works for non-negative inputs when the reversed result fits in an `int`. It does not handle negative input or protect against overflow.

## 5. Handling Negative Numbers

In C++, the remainder has the sign of the left operand:

| Expression | Result |
|---|---:|
| `456 % 10` | 6 |
| `-456 % 10` | -6 |
| `-123 % 10` | -3 |

Therefore, we can use the same digit-processing loop for positive and negative numbers by using `while (n != 0)`. The extracted digits will carry the appropriate sign, and the reversed result will naturally be negative when the input is negative.

We should not blindly use `n = -n` to make every input positive. The most negative 32-bit `int` is `-2147483648`; its positive counterpart, `2147483648`, cannot fit in a 32-bit `int`. Negating it causes signed integer overflow (undefined behavior).

## 6. Understanding Integer Overflow

For a typical 32-bit signed `int`:

- `INT_MAX = 2147483647`
- `INT_MIN = -2147483648`

The negative range has one extra value because the range is asymmetric around zero.

Before executing:

```cpp
reverse = reverse * 10 + digit;
```

we must check whether the next multiplication and addition would go outside the `int` range.

For positive values, when `reverse == INT_MAX / 10`, the final digit must not be greater than `7`, because `INT_MAX` ends in 7.

For negative values, when `reverse == INT_MIN / 10`, the final digit must not be less than `-8`, because `INT_MIN` ends in 8.

The checks must happen **before** the multiplication and addition.

## 7. Complete Overflow-Safe C++ Implementation

This is the complete version that handles positive numbers, negative numbers, zero, and overflow. It returns `0` if the reversed value cannot fit in an `int`.

```cpp
#include <climits>

int reverseNumber(int n) {
    int reverse = 0;

    while (n != 0) {
        int digit = n % 10;

        // Check positive overflow before multiplying by 10.
        if (reverse > INT_MAX / 10 ||
            (reverse == INT_MAX / 10 && digit > 7)) {
            return 0;
        }

        // Check negative overflow before multiplying by 10.
        if (reverse < INT_MIN / 10 ||
            (reverse == INT_MIN / 10 && digit < -8)) {
            return 0;
        }

        reverse = reverse * 10 + digit;
        n = n / 10;
    }

    return reverse;
}
```

**Code explanation:**

1. Initialize `reverse = 0` because no digits have been added yet.
2. Use `while (n != 0)` so both positive and negative inputs are processed.
3. Extract the last digit using `n % 10`.
4. Check the positive overflow boundary using `INT_MAX / 10` and the final-digit limit `7`.
5. Check the negative overflow boundary using `INT_MIN / 10` and the final-digit limit `-8`.
6. Return `0` if either check shows that the next operation would overflow.
7. Otherwise, append the digit using `reverse = reverse * 10 + digit`.
8. Remove the processed digit using `n = n / 10`.
9. Return the reversed number after all digits are processed.

The `<climits>` header provides `INT_MAX` and `INT_MIN`. These limits describe the range of the `int` type on the platform; the values above are for a typical 32-bit `int`.

## 8. Examples and Dry Runs

### Example A: Positive number

Input: `1234`

| Iteration | `n` before | `digit = n % 10` | `reverse` after update |
|---|---:|---:|---:|
| 1 | 1234 | 4 | 4 |
| 2 | 123 | 3 | 43 |
| 3 | 12 | 2 | 432 |
| 4 | 1 | 1 | 4321 |

Output: `4321`.

### Example B: Negative number

Input: `-456`

| Iteration | `n` before | `digit = n % 10` | `reverse` after update |
|---|---:|---:|---:|
| 1 | -456 | -6 | -6 |
| 2 | -45 | -5 | -65 |
| 3 | -4 | -4 | -654 |

Output: `-654`.

### Example C: Trailing zeroes

Input: `1200`

The extracted digits are `0`, `0`, `2`, and `1`. The reversed value builds as `0 → 0 → 2 → 21`.

Output: `21`.

### Example D: Overflow

Input: `1534236469`

Reversing it would produce `9646324351`, which is greater than `INT_MAX`. The function detects this before performing the overflowing operation and returns `0`.

## 9. Important Edge Cases

| Input | Output | Reason |
|---:|---:|---|
| 0 | 0 | No loop iteration is needed |
| 5 | 5 | Single digit |
| 1200 | 21 | Leading zeroes are not represented |
| -456 | -654 | Negative digits retain their sign |
| 1534236469 | 0 | Reversed value exceeds `INT_MAX` |
| -2147483648 | 0 | Reversed value cannot fit in `int` |

The overflow-safe implementation assumes the conventional problem requirement that an out-of-range reversed result should return `0`.

## 10. Time Complexity

Let `d` be the number of digits in the input. Each loop iteration processes exactly one digit.

**Time Complexity: `O(d)`**, or `O(log₁₀ |n|)` for non-zero `n`.

## 11. Auxiliary Space Complexity

The algorithm uses a fixed number of integer variables and does not allocate an extra array or data structure.

**Auxiliary Space Complexity: `O(1)`**.

## 12. Common Mistakes

1. **Using `while (n > 0)`:** this stops immediately for negative numbers. Use `while (n != 0)` in the signed implementation.
2. **Forgetting to remove a digit:** without `n = n / 10`, the loop does not make progress.
3. **Using the wrong order of operations:** extract the digit, check overflow, append it, then remove it from `n`.
4. **Negating every negative input:** `-INT_MIN` cannot be represented as an `int`.
5. **Checking overflow after the calculation:** overflow must be checked before multiplying and adding.
6. **Using the wrong boundary digits:** the positive limit ends in `7`; the negative limit ends in `8`.
7. **Forgetting that leading zeroes disappear:** reversing `1200` produces `21`, not `0021`.

## 13. Practice Problems

1. Reverse `456`.
2. Reverse `9005`.
3. Reverse `-123`.
4. What does the function return for `0`?
5. Explain why reversing `1534236469` returns `0`.
6. Trace the function for `-120`.
7. Explain why `INT_MIN` cannot safely be negated as an `int`.

## 14. Interview Patterns

- **Digit Extraction:** `n % 10` and `n / 10` are the basic pattern.
- **Build a Number:** `reverse * 10 + digit` appends a digit to a result.
- **Palindrome Number:** reverse the number and compare it with the original, while considering overflow and input constraints.
- **Overflow Prevention:** check the boundary before performing an operation that may exceed the integer type's range.

## 15. Revision Summary

- `n % 10` extracts the last digit.
- `n / 10` removes the last digit.
- `reverse = reverse * 10 + digit` appends the digit to the reversed number.
- Use `n != 0` to process both positive and negative numbers.
- Negative modulo results are negative in C++ when the left operand is negative.
- Do not negate `INT_MIN` as an `int`.
- Check against `INT_MAX` and `INT_MIN` **before** updating the reversed number.
- Time complexity: `O(d)`.
- Auxiliary space complexity: `O(1)`.

### Final Memory Trick

```text
n % 10                    → Extract the last digit
reverse * 10 + digit      → Append it to the reversed number
n / 10                    → Remove the processed digit
Overflow check            → Protect the int range before updating
```
