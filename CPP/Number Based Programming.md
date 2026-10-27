# Number Based Programming

## Topic 1: Digit Extraction

**Status:** Lesson and practice completed

### 1. What Is Digit Extraction?

Digit extraction means taking the individual digits of a number one at a time.

For example, for the number `472`, the digits are extracted from right to left:

```text
2
7
4
```

### 2. Why Do We Need It?

Digit extraction is the foundation for number-based problems such as:
- Counting digits
- Finding the sum of digits
- Reversing a number
- Checking palindrome numbers
- Checking Armstrong numbers

### 3. Core Intuition

We use two operators: modulo (`%`) and integer division (`/`).

**Modulo (`% 10`) — extracts the last digit**

```cpp
472 % 10 = 2
```

**Integer division (`/ 10`) — removes the last digit**

```cpp
472 / 10 = 47
```

Because both operands are integers, the fractional part is discarded.

| Operation | Purpose | Example |
|---|---|---|
| `n % 10` | Extract the last digit | `472 % 10 = 2` |
| `n / 10` | Remove the last digit | `472 / 10 = 47` |

### 4. C++ Implementation

This is the digit-extraction program we learned:

```cpp
#include<iostream>
using namespace std ;

int main(){
    int n;
    cin >> n;

    while(n > 0){
        int digit = n % 10;
        cout << digit << endl;
        n = n / 10;
    }

    return 0;
}
```

**Code explanation:**
1. Read an integer into `n`.
2. The loop runs while `n > 0`.
3. `n % 10` extracts the last digit and stores it in `digit`.
4. Print the extracted digit.
5. `n / 10` removes the last digit.
6. Repeat until `n` becomes zero.

### 5. Example

**Input**
```text
472
```

**Output**
```text
2
7
4
```

Digits are printed from right to left because the last digit is extracted first.

### 6. Dry Run

For `n = 472`:

| Iteration | `n` | `n % 10` (digit) | `n / 10` (updated value) |
|---|---:|---:|---:|
| 1 | 472 | 2 | 47 |
| 2 | 47 | 7 | 4 |
| 3 | 4 | 4 | 0 |

When `n` becomes `0`, the condition `n > 0` is false and the loop stops.

**Example with an internal zero:** for input `1205`, the extracted digits are `5 0 2 1`. The zero inside the number is extracted correctly.

### 7. Handling the Edge Case: Input Is Zero

With only `while(n > 0)`, an input of `0` prints nothing because the loop condition is false immediately.

This is the version we wrote to handle zero:

```cpp
#include<iostream>
using namespace std ;

int main(){
    int n;
    cin >> n;

    if(n == 0) cout << 0;

    while(n > 0){
        int digit = n % 10;
        cout << digit << " ";
        n = n / 10;
    }

    return 0;
}
```

If `n == 0`, the `if` statement prints `0`. The loop is then skipped. For a positive number, the loop extracts each digit normally.

This program supports nonnegative integers within the `int` range.

### 8. Time Complexity

Let `d` be the number of digits in the number. Each loop iteration processes one digit.

**Time Complexity: `O(d)`**

### 9. Space Complexity

Only a few integer variables are used; no extra array or data structure is needed.

**Auxiliary Space Complexity: `O(1)`**

### 10. Common Mistakes

1. **Using `n / 10` to extract a digit:** use `n % 10` to extract the last digit.
2. **Forgetting to update `n`:** without `n = n / 10`, the loop can run forever.
3. **Forgetting the zero edge case:** `while(n > 0)` does not execute when `n == 0`; handle zero separately if it must be printed.
4. **Expecting left-to-right output:** digits are extracted from right to left.

### 11. Practice Problems

1. Predict the extracted digits for `583`.
2. Predict the extracted digits for `406`.
3. Predict the extracted digits for `1205`.
4. Explain the value of `n` after each iteration for `651`.
5. Write a program that extracts digits from right to left and handles input `0`.

### 12. Interview Patterns

Digit extraction is a building block for:
- **Count Digits:** count how many times digits are processed.
- **Sum of Digits:** add each extracted digit.
- **Reverse a Number:** build a new number from extracted digits.
- **Palindrome Number:** reverse the number and compare it with the original.
- **Armstrong Number:** process each digit and calculate its required power.

### 13. Revision Summary

- `n % 10` extracts the last digit.
- `n / 10` removes the last digit through integer division.
- `while(n > 0)` processes the digits of a positive number.
- Digits are extracted from right to left.
- Handle `n == 0` separately when zero must be printed.
- Time complexity: `O(d)`, where `d` is the number of digits.
- Auxiliary space complexity: `O(1)`.

### Final Memory Trick

```text
n % 10  → Extract
n / 10  → Remove
```
