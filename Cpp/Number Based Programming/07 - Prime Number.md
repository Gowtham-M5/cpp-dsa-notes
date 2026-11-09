# Prime Number — Complete DSA Notes (C++)

## 1. What is a prime number?

A **prime number** is a positive integer greater than 1 that has exactly two distinct positive factors:

1. 1
2. The number itself

Examples:
- 2: factors are 1 and 2 → prime
- 3: factors are 1 and 3 → prime
- 5: factors are 1 and 5 → prime
- 7: factors are 1 and 7 → prime

A **composite number** is a positive integer greater than 1 that has more than two positive factors.

Examples:
- 4: factors are 1, 2, 4 → composite
- 6: factors are 1, 2, 3, 6 → composite
- 9: factors are 1, 3, 9 → composite

Important facts:
- 1 is neither prime nor composite because it has exactly one positive factor.
- 0 and negative integers are not prime.
- 2 is the smallest prime number and the only even prime number.
- Every even integer greater than 2 is composite.

## 2. Why do we need to check divisors?

To decide whether n is prime, we check whether any integer from 2 up to (but not including) n divides n exactly.

In C++, the modulo operator \`%\` gives the remainder:
- If \`n % i == 0\`, then i divides n completely. So n is not prime.
- If no divisor is found, n is prime.

## 3. Brute-force approach

### Intuition

Try every possible divisor from 2 to n - 1.
- If any divisor divides n, immediately return \`false\`.
- If the loop finishes without finding a divisor, return \`true\`.

### C++ implementation

\`\`\`cpp
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }

    for (int i = 2; i < n; i++) {
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}
\`\`\`

### Dry run: n = 9

| i | 9 % i | What happens? |
|---|---:|---|
| 2 | 1 | Not divisible; continue |
| 3 | 0 | Divisor found; return false |

So 9 is not prime.

### Dry run: n = 7

| i | 7 % i | What happens? |
|---|---:|---|
| 2 | 1 | Continue |
| 3 | 1 | Continue |
| 4 | 3 | Continue |
| 5 | 2 | Continue |
| 6 | 1 | Continue |

No divisor is found, so the function returns \`true\`.

### Complexity

- **Time:** O(n), because in the worst case (when n is prime) we test all integers from 2 to n - 1.
- **Auxiliary space:** O(1), because we use only a few variables.

## 4. Optimized approach: check only up to the square root

### Core intuition

Factors occur in pairs.

For example, factor pairs of 36 are:
- 1 × 36
- 2 × 18
- 3 × 12
- 4 × 9
- 6 × 6

The pairs meet at √36 = 6. After that point, the same pairs appear in reverse order.

More generally, if n = a × b and both a and b were greater than √n, their product would be greater than n. Therefore, at least one factor in every factor pair must be less than or equal to √n.

So, if no divisor is found from 2 through √n, no larger divisor can exist without a matching smaller divisor. We only need to check up to the square root.

### Loop condition

A common integer-only condition is:

\`\`\`cpp
i * i <= n
\`\`\`

This includes the square-root boundary. The equality is important:
- For n = 25, i reaches 5.
- \`5 * 5 <= 25\` is true, so 5 is checked.
- Since \`25 % 5 == 0\`, the function correctly returns false.
- If we used \`i * i < n\`, the divisor 5 would be skipped and 25 could be incorrectly classified as prime.

We do not check “half of n”; we check up to √n.

### C++ implementation using i * i <= n

\`\`\`cpp
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }

    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}
\`\`\`

### Dry run: n = 49

√49 = 7.

| i | i * i <= 49? | 49 % i | What happens? |
|---|---|---:|---|
| 2 | true | 1 | Continue |
| 3 | true | 1 | Continue |
| 4 | true | 1 | Continue |
| 5 | true | 4 | Continue |
| 6 | true | 1 | Continue |
| 7 | true | 0 | Return false |

49 is not prime.

### Dry run: n = 35

√35 is approximately 5.916, so the integer loop checks i = 2, 3, 4, 5.

At i = 5, \`35 % 5 == 0\`, so the function returns false. The square root does not need to be an integer.

### Complexity

- **Time:** O(√n), because at most about √n divisors are checked.
- **Auxiliary space:** O(1).

This is substantially faster than the brute-force O(n) approach for large n.

## 5. A note about integer overflow in the loop condition

For ordinary learning examples, \`i * i <= n\` clearly expresses the square-root idea. However, multiplication can overflow for sufficiently large integer types or values.

A safer equivalent condition for positive n is:

\`\`\`cpp
i <= n / i
\`\`\`

It avoids multiplying i by itself.

A robust implementation for an \`int\` input is:

\`\`\`cpp
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }

    for (int i = 2; i <= n / i; i++) {
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}
\`\`\`

For the current learning stage, understand both forms. The important mathematical idea is still that we only need to test divisors up to √n.

## 6. Test cases and edge cases

| Input n | Expected result | Reason |
|---:|---|---|
| -5 | false | Negative numbers are not prime |
| 0 | false | Prime numbers must be greater than 1 |
| 1 | false | It has only one positive factor |
| 2 | true | Factors: 1 and 2 |
| 3 | true | Factors: 1 and 3 |
| 4 | false | Divisible by 2 |
| 7 | true | No divisor other than 1 and itself |
| 9 | false | Divisible by 3 |
| 25 | false | Divisible by 5; square-root boundary |
| 49 | false | Divisible by 7; square-root boundary |
| 35 | false | Divisible by 5 and 7 |

## 7. Common mistakes

1. **Forgetting the n <= 1 check:** 1, 0, and negative values must return false.
2. **Starting the loop at 1:** Every integer is divisible by 1, so this does not help identify prime numbers.
3. **Checking n itself:** Every number is divisible by itself, so the brute-force loop uses \`i < n\`.
4. **Returning true inside the loop:** This may classify a number as prime after checking only one possible divisor. Return true only after the loop finishes.
5. **Using < instead of <= in the square-root condition:** Perfect squares such as 25 and 49 may have their square-root divisor skipped.
6. **Confusing √n with n / 2:** The optimized limit is the square root, not half the number.
7. **Forgetting that 2 is prime:** It is the only even prime number.
8. **Potential overflow in \`i * i\`:** For robust code, use \`i <= n / i\` after handling n <= 1.

## 8. Interview and problem-solving patterns

Prime checking connects to several common DSA patterns:
- **Early return:** Stop immediately when a divisor is found.
- **Square-root optimization:** Reduce a divisor search from O(n) to O(√n).
- **Modulo:** Use \`%\` to test divisibility.
- **Boundary conditions:** Handle n <= 1 and perfect squares carefully.
- **Repeated prime checks:** For many queries or ranges, learn the Sieve of Eratosthenes later; it is more efficient than independently checking every number.

## 9. Practice problems (in increasing difficulty)

1. Write \`isPrime(n)\` using the brute-force approach.
2. Optimize \`isPrime(n)\` using the square-root condition.
3. Print all prime numbers from 1 to n.
4. Count the prime numbers in a given range.
5. Find the smallest prime number greater than n.
6. Learn and implement the Sieve of Eratosthenes for many prime queries.

Do not jump to the sieve until the single-number prime-checking logic is comfortable.

## 10. Revision summary

- A prime number is an integer greater than 1 with exactly two positive factors.
- 1 is neither prime nor composite.
- Use \`n % i == 0\` to detect a divisor.
- Brute force checks i from 2 to n - 1: O(n) time and O(1) space.
- The factor-pair property proves that checking only through √n is sufficient.
- Use \`i * i <= n\` to include the square-root boundary; \`i <= n / i\` avoids multiplication overflow.
- Optimized prime checking takes O(√n) time and O(1) auxiliary space.

## 11. Learning progress

- [x] Prime number definition and classification
- [x] Brute-force C++ implementation
- [x] Dry runs
- [x] Square-root optimization
- [x] Complexity analysis
- [x] Edge cases and common mistakes
- [x] Practice roadmap

**Status:** Prime Number topic covered in Phase 1.
