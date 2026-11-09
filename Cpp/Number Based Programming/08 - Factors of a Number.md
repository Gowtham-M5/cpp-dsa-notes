# Factors of a Number — Complete DSA Notes (C++)

## 1. What is a factor?

A **factor** of a positive integer n is a positive integer that divides n exactly, leaving remainder 0.

In C++, test this with:

```cpp
n % i == 0
```

For example, factors of 12 are **1, 2, 3, 4, 6, 12** because each divides 12 without a remainder.

A factor pair multiplies to n: (1, 12), (2, 6), (3, 4).

## 2. Why do we need factors?

Factors help us:
- Decide whether a number is prime or composite.
- Understand divisibility and factor pairs.
- Build toward GCD, LCM, prime factorization, and divisor-counting problems.

Connection to the previous topic: a prime number has exactly two positive factors: 1 and itself. A composite number greater than 1 has more than two.

## 3. Brute-force approach

### Intuition

Try every integer from 1 through n. If `n % i == 0`, print i.

### C++ implementation

```cpp
void printFactors(int n) {
    if (n <= 0) {
        return;
    }

    for (int i = 1; i <= n; i++) {
        if (n % i == 0) {
            cout << i << " ";
        }
    }
}
```

### Dry run: n = 10

| i | 10 % i | Result |
|---:|---:|---|
| 1 | 0 | Print 1 |
| 2 | 0 | Print 2 |
| 3 | 1 | Skip |
| 4 | 2 | Skip |
| 5 | 0 | Print 5 |
| 6 | 4 | Skip |
| 7 | 3 | Skip |
| 8 | 2 | Skip |
| 9 | 1 | Skip |
| 10 | 0 | Print 10 |

Output: `1 2 5 10`

**Time:** O(n), because we test every integer from 1 to n.  
**Auxiliary space:** O(1), because we use only a loop variable and no extra collection.

## 4. Optimized approach: factor pairs and square root

### Core intuition

Factors appear in pairs. For n = 36:

- 1 × 36
- 2 × 18
- 3 × 12
- 4 × 9
- 6 × 6

The pairs meet at √36 = 6. After that, the larger partners repeat in reverse order.

For any factor pair a × b = n, at least one factor must be less than or equal to √n. Otherwise both would be greater than √n and their product would exceed n.

So we only need to search for the smaller factors up to √n. For every divisor i, its partner is n / i.

### Why use two loops?

A single loop can print pairs like `1 36 2 18 3 12...`, which is not sorted.

To print factors in ascending order without an array:
1. First loop: print the smaller factors in increasing order.
2. Second loop: walk back down from √n and print each larger partner. This prints the partners in increasing order.
3. If i equals n / i, it is the square-root factor and must not be printed twice.

### C++ implementation

```cpp
#include <iostream>
#include <cmath>
using namespace std;

void printFactors(int n) {
    if (n <= 0) {
        return;
    }

    int limit = static_cast<int>(sqrt(n));

    // Print smaller factors in ascending order.
    for (int i = 1; i <= limit; i++) {
        if (n % i == 0) {
            cout << i << " ";
        }
    }

    // Print larger partners in ascending order.
    for (int i = limit; i >= 1; i--) {
        if (n % i == 0 && i != n / i) {
            cout << n / i << " ";
        }
    }
}
```

### Dry run: n = 36

First loop, i = 1 through 6:
- 1 divides 36 → print 1
- 2 divides 36 → print 2
- 3 divides 36 → print 3
- 4 divides 36 → print 4
- 5 does not divide 36
- 6 divides 36 → print 6

First part: `1 2 3 4 6`

Second loop, i = 6 down to 1:
- i = 6 → partner 36 / 6 = 6. Skip because it is already printed.
- i = 5 → not a divisor.
- i = 4 → partner 9. Print 9.
- i = 3 → partner 12. Print 12.
- i = 2 → partner 18. Print 18.
- i = 1 → partner 36. Print 36.

Final output: `1 2 3 4 6 9 12 18 36`

### Dry run: n = 24

- Smaller factors through √24: `1 2 3 4`
- Larger partners, traversed in reverse i order: `6 8 12 24`
- Final output: `1 2 3 4 6 8 12 24`

### Complexity

- **Time:** O(√n). Both loops perform at most √n iterations, and constant factors are ignored in Big-O.
- **Auxiliary space:** O(1). No array, vector, or other collection is used.

## 5. Understanding the duplicate check

For a perfect square such as 36, the pair at the boundary is (6, 6). The first loop already prints 6. The second loop must skip it.

`i != n / i` means the two factors are different. If they are equal, do not print the partner again.

## 6. Common mistakes

1. **Starting at 0:** Modulo by zero is invalid. Start at 1.
2. **Forgetting non-positive input:** This implementation prints positive factors only, so it returns for n <= 0.
3. **Printing only i:** In the optimized loop, also consider the paired factor n / i.
4. **Unsorted output:** Printing both members of each pair in one loop produces pair order, not ascending order.
5. **Duplicate square root:** For perfect squares, skip the second copy when `i == n / i`.
6. **Using an array unnecessarily:** Two loops can produce sorted output with O(1) auxiliary space.
7. **Confusing factors and multiples:** Factors divide n; multiples are obtained by multiplying n by an integer.
8. **Overflow in `i * i`:** For large integer values, prefer a division-based loop boundary such as `i <= n / i` when writing an integer-only loop.

## 7. Safer integer-boundary alternative

Instead of calculating a floating-point square root, the first loop can use:

```cpp
for (int i = 1; i <= n / i; i++) {
    if (n % i == 0) {
        cout << i << " ";
    }
}
```

This avoids multiplication overflow. If using this approach for both passes, save the final loop limit (the floor square root) or compute it safely. For this learning implementation, `sqrt(n)` is clear and suitable for ordinary positive `int` inputs.

## 8. Interview patterns

- Divisibility check with modulo.
- Factor-pair reasoning.
- Square-root optimization from O(n) to O(√n).
- Ordered output without sorting or extra storage.
- Duplicate handling at perfect-square boundaries.
- Building blocks for prime checks, GCD/LCM, and prime factorization.

## 9. Practice problems (in increasing difficulty)

1. Print all factors of n using brute force.
2. Count the number of factors of n.
3. Print factors in ascending order using the square-root approach.
4. Check whether n is prime using its factor count.
5. Find the sum of all factors of n.
6. Find the common factors of two numbers.
7. Use common factors to build intuition for GCD.

## 10. Revision summary

- A factor divides n exactly: `n % i == 0`.
- Brute force checks 1 through n: O(n) time, O(1) auxiliary space.
- Factors come in pairs: i and n / i.
- One factor in every pair is at most √n.
- Two loops print smaller factors first and larger partners afterward, in ascending order.
- Skip the duplicate when `i == n / i`.
- Optimized complexity: O(√n) time and O(1) auxiliary space.

## 11. Learning progress

- [x] Factor definition and divisibility test
- [x] Brute-force implementation
- [x] Factor-pair intuition
- [x] Square-root optimization
- [x] Sorted output using two loops
- [x] Perfect-square duplicate handling
- [x] Dry runs and complexity analysis
- [x] Common mistakes and practice roadmap

**Status:** Factors of a Number topic covered in Phase 1.
