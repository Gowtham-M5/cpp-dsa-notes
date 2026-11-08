# 7. Left Rotate by k — Temporary Vector

## Intuition
For a left rotation, the first k values move to the end. Save them first, shift the rest left, then copy the saved values to the back.

## C++ code
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n, k;
    cin >> n;

    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    cin >> k;

    if (n > 0) {
        k %= n;
        vector<int> temp;

        for (int i = 0; i < k; i++) {
            temp.push_back(a[i]);
        }

        for (int i = 0; i < n - k; i++) {
            a[i] = a[i + k];
        }

        for (int i = 0; i < k; i++) {
            a[n - k + i] = temp[i];
        }
    }

    for (int value : a) {
        cout << value << " ";
    }
    return 0;
}
```

## Dry run
Input: `5 1 2 3 4 5 2`

Save `[1, 2]`, shift the remaining values left, then copy the saved values to the last two positions.

Output: `3 4 5 1 2`

## Complexity
- Time: O(n)
- Extra space: O(k)

## Common mistake
Check that n is not zero before `k %= n`. Modulo also handles k larger than n.
