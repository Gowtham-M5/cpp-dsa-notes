# 1299. Replace Elements with Greatest Element on Right Side

- **Difficulty:** Easy
- **Topic:** Array
- **Pattern:** Right-to-Left Maximum Tracking
- **Status:** Solved — submission accepted
- **Practiced / completed:** 2026-10-31

## Problem

For each element in the array, replace it with the greatest element among the elements to its right. Replace the last element with `-1`.

## My approach

I traversed the array from right to left and used `globalmax` to store the greatest original value seen on the right side.

At each index:

1. Save the current original value in `curmax` before overwriting it.
2. Replace the current array element with `globalmax`.
3. Update `globalmax` using the saved original value.

The initial value of `globalmax` is `-1`, which correctly becomes the replacement for the last element.

## My C++ solution

```cpp
class Solution {
public:
    vector<int> replaceElements(vector<int>& arr) {
        int globalmax=-1;
        for(int i=arr.size()-1;i>=0;i--){
            int curmax=arr[i];
            arr[i]=globalmax;
            globalmax=max(globalmax,curmax);
        }
        return arr;
    }
};
```

## Example

Input: `[17,18,5,4,6,1]`

Output: `[18,6,6,6,1,-1]`

## Important concepts learned

- Right-to-left array traversal.
- Maintaining a running maximum while traversing.
- Saving the original value before overwriting an array element.
- In-place array modification.

## Complexity

- **Time:** O(n) — each element is visited once.
- **Auxiliary space:** O(1) — only two variables are used; the input array is modified in place.

## Key learning

When replacing elements using information from their right side, traversing from right to left allows us to maintain the required maximum as we go.
