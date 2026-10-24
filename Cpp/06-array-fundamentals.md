# Array Fundamentals in C++

An array stores multiple values of the same type in contiguous indexed positions. In DSA, arrays are a foundation for traversal, searching, counting, and many problem-solving patterns.

## 1. Declaration and initialization

```cpp
int nums[5] = {10, 20, 30, 40, 50};
```

This array contains five integers. Its indices are `0` through `4`.

```
Index:  0   1   2   3   4
Value: 10  20  30  40  50
```

Access an element using its index: `nums[2]` is `30`.

## 2. Traversal

Traversal means visiting the elements one by one.

```cpp
for (int i = 0; i < 5; i++) {
    cout << nums[i] << " ";
}
```

Start at index 0 and stop before index 5. Accessing `nums[5]` would be out of bounds.

## 3. Finding the largest and smallest values

```cpp
int largest = nums[0];
int smallest = nums[0];

for (int i = 1; i < 5; i++) {
    if (nums[i] > largest) {
        largest = nums[i];
    }
    if (nums[i] < smallest) {
        smallest = nums[i];
    }
}
```

Start both variables from the first array element, then compare every remaining element.

## 4. Sum and average

```cpp
int sum = 0;

for (int i = 0; i < 5; i++) {
    sum += nums[i];
}

double average = static_cast<double>(sum) / 5;
```

The accumulator `sum` starts at 0. Convert to `double` before division when a fractional average is possible; otherwise integer division can discard the fractional part.

## 5. Linear search

Linear search checks elements from left to right until it finds the target or reaches the end.

```cpp
int target = 30;
bool found = false;

for (int i = 0; i < 5; i++) {
    if (nums[i] == target) {
        found = true;
        break;
    }
}

if (found) {
    cout << "Found";
} else {
    cout << "Not found";
}
```

- `found` is a Boolean flag that records whether the target was found.
- `break` stops the search once a match is found.
- If the loop ends without a match, `found` remains false.

## 6. Classifying values

```cpp
if (nums[i] > 0) {
    // positive
} else if (nums[i] < 0) {
    // negative
} else {
    // zero
}
```

For even and odd integers:

```cpp
if (nums[i] % 2 == 0) {
    // even
} else {
    // odd
}
```

## 7. Count digits using division

This idea was used in the LeetCode problem “Find Numbers with Even Number of Digits.”

```cpp
int num = 482;
int digits = 0;

while (num > 0) {
    digits++;
    num /= 10;
}
// digits is 3
```

Dry run:
- `482 / 10` becomes `48`; count = 1.
- `48 / 10` becomes `4`; count = 2.
- `4 / 10` becomes `0`; count = 3.
- The loop stops when `num > 0` is false.

Use a temporary variable when you need to preserve the original array value for later use. For positive integers, repeated integer division by 10 removes one digit each time. Handle zero separately if you generalize this into a reusable digit-count function, because zero has one digit.

## 8. Array problem-solving habits

- Identify the array length and valid index range.
- Initialize counters and accumulators appropriately.
- Reset a per-element or per-row sum before computing a new total.
- Use a Boolean flag when you need to remember whether something was found.
- Use `break` when continuing the search is unnecessary.
- Decide whether the task needs the value, its index, a count, or a Boolean result.

## Complexity intuition

For an array of `n` elements:
- Accessing an element by index takes constant time, `O(1)`.
- Traversing all elements takes linear time, `O(n)`.
- Linear search takes `O(n)` time in the worst case.
