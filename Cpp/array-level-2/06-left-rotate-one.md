# 6. Left Rotate an Array by One Position

## Intuition
Save the first element, shift each later element one position left, and put the saved element at the end.

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

    if (n > 1) {
        int first = a[0];

        for (int i = 0; i < n - 1; i++) {
            a[i] = a[i + 1];
        }

        a[n - 1] = first;
    }

    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
    return 0;
}
```

## Dry run
Input: `4 10 20 30 40`

Save 10, shift 20/30/40 left, and place 10 at the end.

Output: `20 30 40 10`

## Complexity
- Time: O(n)
- Extra space: O(1)

## Common mistake
Save the first value before shifting or it will be overwritten.
