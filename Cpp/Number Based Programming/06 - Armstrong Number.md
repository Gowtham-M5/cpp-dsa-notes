# Armstrong Number — DSA Notes (C++)

## 1. Definition
An Armstrong number is equal to the sum of each digit raised to the power of the number of digits.

Examples:
- 153: 1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153 (Armstrong)
- 370: 3^3 + 7^3 + 0^3 = 27 + 343 + 0 = 370 (Armstrong)
- 123: 1^3 + 2^3 + 3^3 = 36 (not Armstrong)
- 9474: 9^4 + 4^4 + 7^4 + 4^4 = 9474 (Armstrong)

## 2. Intuition
1. Save the original number because the counting loop modifies n.
2. Count the digits.
3. Copy the original number into temp.
4. Extract each digit using % 10.
5. Calculate digit^count using repeated multiplication.
6. Add each power to sum.
7. Compare sum with the original number.

## 3. C++ Implementation

```cpp
bool isArmstrong(int n) {
    if (n < 0) {
        return false;
    }

    int originalno = n;
    int count = 0;
    long long sum = 0;

    // Zero has one digit.
    if (n == 0) {
        count = 1;
    } else {
        while (n > 0) {
            n = n / 10;
            count++;
        }
    }

    int temp = originalno;

    while (temp > 0) {
        int digit = temp % 10;
        long long power = 1;

        // Calculate digit^count.
        for (int i = 0; i < count; i++) {
            power = power * digit;
        }

        sum += power;
        temp = temp / 10;
    }

    return originalno == sum;
}
```

This handles the usual int-sized learning examples. For unrestricted input sizes, intermediate multiplication can still overflow; use checked arithmetic or a wider/arbitrary-precision type.

## 4. Dry Run: n = 153

Digit counting: 153 -> 15 -> 1 -> 0, so count = 3.

| Digit | Power calculation | Power | Running sum |
|---:|---|---:|---:|
| 3 | 3 x 3 x 3 | 27 | 27 |
| 5 | 5 x 5 x 5 | 125 | 152 |
| 1 | 1 x 1 x 1 | 1 | 153 |

Compare sum == originalno: 153 == 153, so return true.

## 5. Important C++ Concepts
- n % 10 extracts the last digit.
- n / 10 removes the last digit (integer division).
- ^ is bitwise XOR in C++, not exponentiation.
- power must start at 1 for every digit.
- originalno preserves the input; temp is the changing copy.
- Zero is an Armstrong number: its only digit contributes 0.

## 6. Complexity
Let d be the number of digits.
- Counting digits: O(d).
- There are d digits, and each power calculation takes O(d).
- Time complexity: O(d^2).
- Auxiliary space: O(1).

## 7. Test Cases

| Input | Expected |
|---:|---|
| 0 | true |
| 153 | true |
| 370 | true |
| 371 | true |
| 9474 | true |
| 123 | false |
| -153 | false |

## 8. Common Mistakes
1. Using digit ^ count for powers.
2. Reusing n after the digit-count loop; n becomes 0.
3. Not copying originalno into temp.
4. Initializing power only once instead of once per digit.
5. Forgetting to handle negative numbers or zero.

## 9. Revision Summary
**Preserve -> Count -> Copy -> Extract -> Power -> Sum -> Compare**
