# Palindrome Number

## 1. What is it?

A palindrome number reads the same forward and backward. Reversing the digits gives the original number.

Examples:
- `121` → palindrome
- `1221` → palindrome
- `123` → not a palindrome
- `10` → not a palindrome
- `0` → palindrome
- `-121` → not a palindrome

## 2. Why do we need it?

Palindrome checking is a basic number-manipulation problem. It practices digit extraction, number reversal, loops, conditions, and edge-case handling.

## 3. Core intuition

1. Save the original number because the input variable will be changed while extracting digits.
2. Reverse the number one digit at a time:
   - `digit = n % 10` extracts the last digit.
   - `reverse = reverse * 10 + digit` appends that digit to the reversed number.
   - `n = n / 10` removes the last digit.
3. Compare the reversed number with the saved original.
4. If they are equal, the number is a palindrome.

Negative numbers are not considered palindromes in the standard definition used by common DSA problems. The minus sign is part of the number, so `-121` does not read the same backward.

## 4. Basic implementation in C++

The following is the implementation practiced during the lesson:

```cpp
bool isPalindrome(int n) {
    int originalno = n;
    int digit;
    int reverse = 0;

    if (n == 0) {
        return true;
    }

    if (n < 0) {
        return false;
    }

    while (n > 0) {
        digit = n % 10;
        reverse = reverse * 10 + digit;
        n = n / 10;
    }

    if (originalno == reverse) {
        return true;
    }
    else {
        return false;
    }
}
```

## 5. Example

Input: `n = 1221`

- Original number: `1221`
- Reversed number: `1221`
- Comparison: `1221 == 1221`
- Result: `true`

## 6. Dry run

For `n = 123`:

| Iteration | digit = n % 10 | reverse = reverse * 10 + digit | n = n / 10 |
|---|---:|---:|---:|
| Start | — | 0 | 123 |
| 1 | 3 | 3 | 12 |
| 2 | 2 | 32 | 1 |
| 3 | 1 | 321 | 0 |

Now compare:
- `originalno = 123`
- `reverse = 321`
- `123 == 321` is false.

Therefore, `123` is not a palindrome.

## 7. Time complexity

**O(log₁₀ n)** for positive `n`, because the loop processes one digit per iteration and an integer with `d` digits takes `d = O(log₁₀ n)` iterations.

## 8. Space complexity

**O(1)** auxiliary space. Only a fixed number of variables are used.

## 9. Common mistakes

- Not saving the original number before changing `n`.
- Forgetting that `n % 10` extracts the last digit.
- Forgetting to remove the last digit with `n / 10`.
- Not handling negative numbers.
- Forgetting the special case `0`, which is a palindrome.
- Using an `int` reversal without considering overflow for very large inputs. A production/interview implementation should guard the reversal operation against overflow (or use a wider type where appropriate).

## 10. Practice problems

Try these in increasing order:
1. Check whether `7` is a palindrome.
2. Check whether `10` is a palindrome.
3. Check whether `12321` is a palindrome.
4. Check whether `-121` is a palindrome.
5. Implement the check without constructing the entire reversed number (advanced follow-up).

## 11. Interview patterns

- Digit extraction using modulo and division.
- Reversing an integer.
- Comparing a transformed value with the original.
- Edge-case handling for zero, negative values, and integer overflow.

## 12. Revision summary

- A palindrome number equals its reverse.
- Save the original value before modifying the input.
- Extract digits with `% 10` and remove digits with `/ 10`.
- Negative numbers are not palindromes under the standard integer-palindrome definition.
- Time: **O(log₁₀ n)**; auxiliary space: **O(1)**.
