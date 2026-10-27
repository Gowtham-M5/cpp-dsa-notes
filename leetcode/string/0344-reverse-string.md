# LeetCode #344: Reverse String

**Difficulty:** Easy  
**Topic:** Strings  
**Pattern:** Two Pointers + In-place Swapping  
**Status:** Practiced — acceptance not yet confirmed  
**Date:** October 27, 2026

## 1. Problem Statement

Given an array of characters `s`, reverse the array in place.

You must modify the original array without creating another array to store the reversed characters.

**Example**

Input:
```text
s = ['h', 'e', 'l', 'l', 'o']
```

Output:
```text
['o', 'l', 'l', 'e', 'h']
```

## 2. My Approach

I used the **Two Pointers** technique to reverse the string.

1. Initialize `left = 0` to point to the first character.
2. Initialize `right = s.size() - 1` to point to the last character.
3. Use a `while` loop that continues while `left < right`.
4. Swap the characters at `left` and `right`.
5. Increment `left` and decrement `right`.
6. Stop when the pointers meet or cross.

This reverses the character array without requiring another array.

## 3. My Code

```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        int left=0;
        int right=s.size()-1;
        while(left<right){
            swap(s[left],s[right]);
            left++;
            right--;

        }
        
    }
};
```

## 4. Dry Run

Consider the input:

```text
s = ['h', 'e', 'l', 'l', 'o']
```

Initially:
- `left = 0`
- `right = 4`

| Step | Left | Right | Operation | Result |
|---|---:|---:|---|---|
| 1 | 0 | 4 | Swap `h` and `o` | `['o','e','l','l','h']` |
| 2 | 1 | 3 | Swap `e` and `l` | `['o','l','l','e','h']` |
| 3 | 2 | 2 | Stop because `left < right` is false | `['o','l','l','e','h']` |

Final result: `['o', 'l', 'l', 'e', 'h']`

The characters are now in reverse order.

## 5. Important Concepts Learned

### Two Pointers

Two variables, `left` and `right`, track positions in the same array.

- `left` starts at the beginning.
- `right` starts at the end.
- Both pointers move toward the middle.

### Swapping

`swap(s[left], s[right])` exchanges the characters at the two positions.

### In-place Modification

The original array is modified directly. No additional array is required.

### Loop Condition

`while(left < right)` ensures that swapping stops when the pointers meet or cross. If both pointers meet at the middle character, no swap is necessary.

## 6. Time and Space Complexity

**Time Complexity: O(n)**

Each iteration performs one swap, and the pointers move toward the middle. For an array of length `n`, approximately `n/2` swaps are performed. Therefore, the time complexity is O(n).

**Auxiliary Space Complexity: O(1)**

Only a constant amount of additional space is used for the two pointer variables. The original array is modified directly, so no additional array is created. Therefore, the auxiliary space complexity is O(1).

## 7. Pattern Recognition

**Pattern:** Two Pointers

This pattern can be useful when a problem requires:
- Swapping elements from opposite ends.
- Reversing an array or string.
- Processing elements from both ends.
- Modifying an array in place.

**Core idea:** Start with two pointers at opposite ends, perform the required operation, and move both pointers toward each other.

## 8. Revision Summary

1. Initialize pointers at both ends.
2. Swap the elements and move both pointers inward.
3. Stop when `left < right` becomes false.

**Key takeaway:** Two pointers can reverse an array in O(n) time and O(1) auxiliary space.
