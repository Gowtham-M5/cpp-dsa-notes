# 3. Check Whether an Array Is Sorted

## Intuition
Compare each element with the previous element. If the current value is smaller, the array is not in ascending (non-decreasing) order.

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

    bool sorted = true;

    for (int i = 1; i < n; i++) {
        if (a[i] < a[i - 1]) {
            sorted = false;
            break;
        }
    }

    if (sorted) {
        cout << "Sorted";
    } else {
        cout << "Not sorted";
    }
    return 0;
}
```

## Dry run
Input: `4 1 2 2 5`

Compare 2 with 1, 2 with 2, and 5 with 2. No current element is smaller than its previous element, so the array is sorted.

## Complexity
- Time: O(n) worst case
- Extra space: O(1)

## Common mistake
Start comparisons at index 1 because index 0 has no previous element. Equal adjacent values are allowed.
