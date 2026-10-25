# 1. Reverse an Array

## Intuition
Use two pointers: one at the beginning and one at the end. Swap their elements and move both pointers toward the centre.

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

    int left = 0;
    int right = n - 1;

    while (left < right) {
        swap(a[left], a[right]);
        left++;
        right--;
    }

    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
    return 0;
}
```

## Dry run
Input: `5 1 2 3 4 5`

- Swap first and last: `[5, 2, 3, 4, 1]`
- Swap the next pair: `[5, 4, 3, 2, 1]`
- The pointers meet/cross, so stop.

Output: `5 4 3 2 1`

## Complexity
- Time: O(n)
- Extra space: O(1), excluding the input array.

## Common mistake
Use `n - 1` as the last valid index, not `n`.
