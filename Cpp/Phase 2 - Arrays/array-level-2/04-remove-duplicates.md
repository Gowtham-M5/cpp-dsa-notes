# 4. Remove Duplicates from a Sorted Array

## Intuition
The array must already be sorted, so equal values sit beside each other. Keep a write index for the next unique value.

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

    if (n == 0) {
        cout << 0;
        return 0;
    }

    int uniqueCount = 1;

    for (int i = 1; i < n; i++) {
        if (a[i] != a[uniqueCount - 1]) {
            a[uniqueCount] = a[i];
            uniqueCount++;
        }
    }

    for (int i = 0; i < uniqueCount; i++) {
        cout << a[i] << " ";
    }
    cout << "\nUnique count: " << uniqueCount;
    return 0;
}
```

## Dry run
Input: `5 1 1 2 2 3`

- Keep the first 1.
- Skip the next 1.
- Keep 2; skip its duplicate.
- Keep 3.

Unique prefix: `1 2 3`; unique count: `3`.

## Complexity
- Time: O(n)
- Extra space: O(1)

## Common mistake
This in-place method depends on the array being sorted. The unique values occupy the first `uniqueCount` positions; the array's allocated size does not shrink.
