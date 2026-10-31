# 485. Max Consecutive Ones

- **Difficulty:** Easy
- **Topic:** Arrays
- **Pattern:** Counting + Maximum Tracking
- **Status:** Practiced — acceptance not confirmed
- **Practiced on:** 2026-10-31

## Problem

Given a binary array containing only 0s and 1s, find the maximum number of consecutive 1s.

## My approach

I used two counters:

- `count` tracks the current consecutive run of 1s.
- `maxcount` stores the largest run found so far.

I traverse the array once:

1. If the current element is 1, increment `count`.
2. Update `maxcount` if the current run is larger.
3. If the current element is 0, reset `count` to 0 because the consecutive run has ended.
4. Return `maxcount` after the traversal.

## My practiced C++ code

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
       int maxcount=0;
       int count =0;
       for(int i=0;i<nums.size();i++){
        if(nums[i]==1){
            count++;
            maxcount=max(count,maxcount);
        }
        else{
            count=0;
        }
       }
       return maxcount;
    }
};
```

## Example dry run

Input: `[1, 1, 0, 1, 1, 1]`

| Element | Current count | Maximum count |
|---|---:|---:|
| 1 | 1 | 1 |
| 1 | 2 | 2 |
| 0 | 0 | 2 |
| 1 | 1 | 2 |
| 1 | 2 | 2 |
| 1 | 3 | 3 |

Output: `3`

## Important concepts learned

- A counter can track a consecutive sequence.
- Reset the current counter when the sequence is broken.
- Maximum tracking keeps the best value seen during traversal.
- Update the maximum while traversing so that a final run of 1s is also counted.

## Complexity

- **Time:** O(n) — each array element is visited once.
- **Auxiliary space:** O(1) — only two counters are used.

## Revision point

Be able to explain why `count` resets to 0 on encountering a 0, while `maxcount` must not reset.
