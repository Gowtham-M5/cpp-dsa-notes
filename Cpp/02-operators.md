# C++ Operators

An operator performs an operation on one or more values.

## 1. Arithmetic operators

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `5 + 2 == 7` |
| `-` | Subtraction | `5 - 2 == 3` |
| `*` | Multiplication | `5 * 2 == 10` |
| `/` | Division | `5 / 2 == 2` for integers |
| `%` | Remainder | `5 % 2 == 1` |

The remainder operator `%` is useful for checking divisibility and extracting the last digit of an integer.

```cpp
int n = 27;
cout << n % 10; // 7, the remainder after division by 10
cout << n / 10; // 2, integer division removes the last digit
```

This is the basic idea behind counting or processing digits with repeated division by 10.

## 2. Relational/comparison operators

These compare values and produce a Boolean result (`true` or `false`).

- `==`: equal to
- `!=`: not equal to
- `>`: greater than
- `<`: less than
- `>=`: greater than or equal to
- `<=`: less than or equal to

Example:

```cpp
int a = 5;
int b = 8;

cout << (a < b);  // true (usually printed as 1)
cout << (a == b); // false (usually printed as 0)
```

**Important:** `=` assigns a value; `==` compares two values.

## 3. Logical operators

| Operator | Meaning | Example |
|---|---|---|
| `&&` | AND: both conditions must be true | `age >= 18 && age <= 60` |
| `||` | OR: at least one condition must be true | `day == 6 || day == 7` |
| `!` | NOT: reverses a Boolean value | `!isReady` |

Example:

```cpp
int age = 21;
bool hasID = true;

if (age >= 18 && hasID) {
    cout << "Allowed";
}
```

## 4. Assignment and update operators

- `=`: assign a value.
- `+=`: add and store; `sum += x` means `sum = sum + x`.
- `-=`: subtract and store.
- `++`: increase by one.
- `--`: decrease by one.

```cpp
int count = 3;
count++;      // count becomes 4
count += 2;   // count becomes 6
count--;      // count becomes 5
```

## 5. Operator use in DSA

```cpp
if (nums[i] % 2 == 0) {
    // The value is even
}
```

- `% 2 == 0` checks whether an integer is even.
- `% 2 != 0` checks whether it is odd.
- `nums[i] > largest` can be used when finding the largest element.
- `nums[i] == target` checks for a matching value.

## Remember

Before writing a condition, ask yourself:
1. Am I assigning a value or comparing two values?
2. Should all conditions be true (`&&`) or just one (`||`)?
3. What Boolean result will this expression produce?
