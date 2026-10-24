# C++ Loops

Loops repeat a block of code. They are essential for traversing arrays and processing values.

## 1. `for` loop

Use a `for` loop when the repetition follows a clear initialization, condition, and update.

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << " ";
}
```

Output: `0 1 2 3 4`

The three parts are:
- Initialization: `int i = 0` runs once.
- Condition: `i < 5` is checked before each iteration.
- Update: `i++` runs after each iteration.

Trace:
- Start with `i = 0`; condition true; print 0; increment to 1.
- Continue while `i < 5`.
- When `i = 5`, the condition is false and the loop stops.

## 2. `while` loop

A `while` loop repeats as long as its condition is true.

```cpp
int i = 0;
while (i < 5) {
    cout << i << " ";
    i++;
}
```

This produces the same output as the previous example. The initialization is outside the loop and the update is inside it.

## 3. `do-while` loop

A `do-while` loop checks its condition after running the body, so it executes at least once.

```cpp
int i = 0;
do {
    cout << i << " ";
    i++;
} while (i < 5);
```

Remember the semicolon after the `while (i < 5)` in a `do-while` loop.

## 4. Looping through an array

```cpp
int nums[] = {4, 7, 2, 9};
int n = 4;

for (int i = 0; i < n; i++) {
    cout << nums[i] << " ";
}
```

- Array indices start at `0`.
- The last valid index for an array of length `n` is `n - 1`.
- Use `i < n`, not `i <= n`, to avoid accessing index `n), which is outside the array.

## 5. Accumulator pattern: sum of elements

```cpp
int nums[] = {4, 7, 2};
int sum = 0;

for (int i = 0; i < 3; i++) {
    sum += nums[i];
}

cout << sum; // 13
```

The accumulator starts at 0 and grows by adding each element. Reset it when starting a new independent total, such as summing a different customer's row in a 2D array.

## 6. Finding the largest element

```cpp
int nums[] = {4, 7, 2, 9, 3};
int largest = nums[0];

for (int i = 1; i < 5; i++) {
    if (nums[i] > largest) {
        largest = nums[i];
    }
}

cout << largest; // 9
```

Start with the first actual element rather than assuming the largest is 0. This also works when all values are negative.

## 7. `break` and `continue`

- `break` exits the nearest loop immediately.
- `continue` skips the remaining statements in the current iteration and moves to the next iteration.

```cpp
for (int i = 0; i < 5; i++) {
    if (i == 3) {
        break;
    }
    cout << i << " ";
}
// Output: 0 1 2
```

## 8. Avoiding infinite loops

Make sure the loop condition can eventually become false. For example, if the condition is `i < 5`, update `i` so it moves toward or past 5.

## Remember

For every loop, identify:
1. Where does it start?
2. What condition keeps it running?
3. What changes each iteration?
4. When does it stop?
