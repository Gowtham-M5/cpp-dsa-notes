# 8. Right Rotate by k — Temporary Vector

## Intuition
For a right rotation, the last k values move to the front. Save that suffix, shift the other values right from the end toward the beginning, then copy the saved values to the front.

## C++ code
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n, k;
    cin >> n;

    vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }
    cin >> k;

    if (n > 0) {
        k %= n;
        vector<int> temp(k);

        for (int i = 0; i < k; i++) {
            temp[i] = nums[n - k + i];
        }

        for (int i = n - 1; i >= k; i--) {
            nums[i] = nums[i - k];
        }

        for (int i = 0; i < k; i++) {
            nums[i] = temp[i];
        }
    }

    for (int value : nums) {
        cout << value << " ";
    }
    return 0;
}
```

## Dry run
Input: `5 1 2 3 4 5 2`

Save `[4, 5]`; shift the other values right by two; copy `[4, 5]` to the front.

Output: `4 5 1 2 3`

## Complexity
- Time: O(n)
- Extra space: O(k)

## Common mistake
Shift right from the last index backwards. Moving forward can overwrite values that have not yet been moved.
