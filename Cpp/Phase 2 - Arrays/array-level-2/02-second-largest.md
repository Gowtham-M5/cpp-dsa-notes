# 2. Find the Second-Largest Distinct Element

## Intuition
Track the largest and second-largest distinct values in one pass. A duplicate of the largest is not the second-largest.

## C++ code
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    int a[n];
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    int largest = a[0];
    int secondLargest;
    bool foundSecond = false;

    for (int i = 1; i < n; i++) {
        if (a[i] > largest) {
            secondLargest = largest;
            largest = a[i];
            foundSecond = true;
        } else if (a[i] < largest &&
                   (!foundSecond || a[i] > secondLargest)) {
            secondLargest = a[i];
            foundSecond = true;
        }
    }

    if (foundSecond) {
        cout << secondLargest;
    } else {
        cout << "No second-largest distinct element";
    }
    return 0;
}
```

## Dry run
Input: `5 8 8 3 6 2`

- First value: largest = 8.
- Next 8 is equal to largest, so it is ignored.
- 3 becomes second-largest.
- 6 is greater than 3 but less than 8, so second-largest becomes 6.
- 2 does not change the answer.

Output: `6`

## Complexity
- Time: O(n)
- Extra space: O(1)

## Common mistake
Do not count the same maximum value twice. This example assumes `n >= 1`.
