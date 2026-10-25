# 5. Move Zeroes to the End

## Intuition
Copy non-zero values toward the front in their original order. Fill all remaining positions with zero.

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

    int index = 0;

    for (int i = 0; i < n; i++) {
        if (a[i] != 0) {
            a[index] = a[i];
            index++;
        }
    }

    while (index < n) {
        a[index] = 0;
        index++;
    }

    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
    return 0;
}
```

## Dry run
Input: `5 0 1 0 3 12`

Copy 1, 3, and 12 forward, then fill the last two positions with zeroes.

Output: `1 3 12 0 0`

## Complexity
- Time: O(n)
- Extra space: O(1)

## Common mistake
Do not reorder the non-zero elements; their relative order should remain the same.
