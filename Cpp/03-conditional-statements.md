# C++ Conditional Statements

Conditional statements let a program choose which code to execute based on a condition.

## 1. `if`

Use `if` when a block should execute only when a condition is true.

```cpp
int age = 21;

if (age >= 18) {
    cout << "Adult";
}
```

If `age >= 18` is true, the message is printed. Otherwise, the block is skipped.

## 2. `if-else`

Use `else` for the alternative when the `if` condition is false.

```cpp
int number = 7;

if (number % 2 == 0) {
    cout << "Even";
} else {
    cout << "Odd";
}
```

Dry run:
- `7 % 2` is `1`.
- `1 == 0` is false.
- The `else` block prints `Odd`.

## 3. `else if`

Use `else if` to test multiple conditions in order.

```cpp
int marks = 82;

if (marks >= 90) {
    cout << "A";
} else if (marks >= 75) {
    cout << "B";
} else if (marks >= 50) {
    cout << "C";
} else {
    cout << "Needs improvement";
}
```

The first true condition wins; later branches are skipped. Put conditions in an order that matches the logic.

## 4. Nested `if`

An `if` can appear inside another `if` when a decision depends on an earlier decision.

```cpp
int age = 20;
bool hasID = true;

if (age >= 18) {
    if (hasID) {
        cout << "Entry allowed";
    }
}
```

## 5. `switch`

Use `switch` when one expression is compared against several fixed case values.

```cpp
int day = 2;

switch (day) {
    case 1:
        cout << "Monday";
        break;
    case 2:
        cout << "Tuesday";
        break;
    case 3:
        cout << "Wednesday";
        break;
    default:
        cout << "Unknown day";
}
```

- The matching `case` executes.
- `break` exits the switch. Without it, execution may continue into the next case.
- `default` runs when no case matches.
- `switch` is suitable for discrete case values; use `if-else` for ranges such as `marks >= 75`.

## 6. Conditions and Boolean results

Comparison operators such as `==`, `!=`, `<`, and `>=` create Boolean conditions. Logical operators combine them.

```cpp
if (number >= 1 && number <= 10) {
    cout << "In range";
}
```

## Remember

- Use `if` for a single decision, `if-else` for two alternatives, and `else if` for multiple ordered conditions.
- Use `switch` when selecting among fixed values.
- Use braces consistently so the block boundaries are clear.
- Trace the condition first, then decide which block executes.
