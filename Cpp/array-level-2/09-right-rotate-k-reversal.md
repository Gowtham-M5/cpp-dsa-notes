# 9. Right Rotate by k — Reversal Algorithm

## Intuition
Three reversals move the last k values to the front while preserving their internal order.

1. Reverse the whole array.
2. Reverse the first k values.
3. Reverse the remaining values.

## C++ code
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void reverseRange(vector<int>& nums, int left, int right) {
    while (left < right) {
        swap(nums[left], nums[right]);
        left++;
        right--;
    }
}

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
        reverseRange(nums, 0, n - 1);
        reverseRange(nums, 0, k - 1);
        reverseRange(nums, k, n - 1);
    }

    for (int value : nums) {
        cout << value << " ";
    }
    return 0;
}
```

## Dry run
`[1, 2, 3, 4, 5]`, k = 2

1. Reverse all → `[5, 4, 3, 2, 1]`
2. Reverse first two → `[4, 5, 3, 2, 1]`
3. Reverse the rest → `[4, 5, 1, 2, 3]`

## Complexity
- Time: O(n)
- Extra space: O(1), excluding the input vector.

## Common mistake
The right-rotation order is reverse all, then the first k, then the rest.
