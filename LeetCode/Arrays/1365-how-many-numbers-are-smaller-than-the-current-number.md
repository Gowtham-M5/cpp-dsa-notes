# 1365. How Many Numbers Are Smaller Than the Current Number

- **Difficulty:** Easy
- **Topic:** Arrays
- **Pattern:** Nested loops + Counting
- **Status:** Practiced — acceptance not confirmed
- **Practiced on:** 2026-10-31

## Problem

For each element in the input array, count how many elements in the array are strictly smaller than it. Return the counts in the same order as the original elements.

## My approach

I used two nested loops:

1. The outer loop selects the current element, `nums[i]`.
2. Set `count = 0` for that element.
3. The inner loop compares it with every element, `nums[j]`.
4. If `nums[i] > nums[j]`, increment `count`.
5. Store the count at the same index in `result[i]`.
6. Return the result vector.

This preserves the original order because each answer is stored at the index of its corresponding input element.

## My practiced C++ code

```cpp
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
      vector<int> result(nums.size());
      for(int i=0;i<nums.size();i++){
        int count=0;
        for(int j=0;j<nums.size();j++){
            if(nums[i]>nums[j]){
                 count++;
            }
        }
        result[i]=count;
      }
      return result;
    }
};
```

## Example dry run

Input: `[8, 1, 2, 2, 3]`

- For 8: four numbers are smaller → 4
- For 1: no numbers are smaller → 0
- For the first 2: only 1 is smaller → 1
- For the second 2: only 1 is smaller → 1
- For 3: 1, 2, and 2 are smaller → 3

Output: `[4, 0, 1, 1, 3]`

## Important concepts learned

- Nested-loop array traversal.
- Counting elements that satisfy a condition.
- Store each result at the corresponding input index to preserve order.
- The strict comparison `nums[i] > nums[j]` naturally excludes equal values.
- An additional `i != j` check is unnecessary: when `i == j`, an element cannot be strictly greater than itself.

## Complexity

- **Time:** O(n²) — for each of the n elements, the inner loop checks n elements.
- **Auxiliary space:** O(1), excluding the output.
- **Output space:** O(n) for the result vector.

## Revision point

Understand why the inner loop must compare against every element and why the count is reset for every outer-loop iteration.
