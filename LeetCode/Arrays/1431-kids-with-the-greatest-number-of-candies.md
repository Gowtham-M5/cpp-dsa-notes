# 1431. Kids With the Greatest Number of Candies

- **LeetCode:** [1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)
- **Difficulty:** Easy
- **Topic:** Array
- **Status:** Solved — submission accepted (user confirmed on 2026-11-02)
- **Pattern:** Maximum Tracking + Array Traversal
- **Language:** C++

---

## 1. Problem Understanding

Each element in `candies` represents the number of candies a child has. We are given some extra candies.

For every child, determine whether giving all the extra candies to that child would make their total greater than or equal to the current maximum number of candies.

Return the answers as a `vector<bool>`:
- `true` if the child could have the greatest number of candies.
- `false` otherwise.

## 2. Approach Used

The solution uses two traversals.

### Pass 1: Find the current maximum

1. Initialize `max = 0`.
2. Traverse the `candies` array.
3. If the current child's candies are greater than `max`, update `max`.
4. After this loop, `max` contains the greatest current candy count.

### Pass 2: Check each child

1. Create an empty `vector<bool> result`.
2. For each child, calculate `candies[i] + extraCandies`.
3. If this value is greater than or equal to `max`, append `true`.
4. Otherwise, append `false`.
5. Return `result`.

We use `>=` because a child qualifies even when their new total is exactly equal to the current maximum.

## 3. My Accepted C++ Solution

```cpp
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {
        int max=0;
        vector<bool> result;
        for(int i=0;i<candies.size();i++){
            if(candies[i]>max){
                max=candies[i];
            }
        }
        for(int i=0;i<candies.size();i++){
            if(candies[i]+extraCandies>=max){
               result.push_back(true);
            }
            else{
               result.push_back(false);
            }
        }
       return result ; 
    }
};
```

## 4. Important C++ Concept: Why a Separate Result Vector?

The function signature says:

```cpp
vector<bool> kidsWithCandies(...)
```

So the function must return a `vector<bool>`.

But `candies` is a `vector<int>`. We cannot return it because the vector element types do not match.

Instead, we create:

```cpp
vector<bool> result;
```

Then append one Boolean answer for every child:

```cpp
result.push_back(true);
```

or

```cpp
result.push_back(false);
```

Finally, return `result`.

This also keeps the original `candies` array unchanged.

## 5. Dry Run

Example:

```text
candies = [2, 3, 5, 1, 3]
extraCandies = 3
```

### First traversal: find maximum

The maximum value is `5`.

### Second traversal: check each child

| Child index | Candies | After extra candies | Is it >= 5? | Result |
|---:|---:|---:|---|---|
| 0 | 2 | 2 + 3 = 5 | Yes | true |
| 1 | 3 | 3 + 3 = 6 | Yes | true |
| 2 | 5 | 5 + 3 = 8 | Yes | true |
| 3 | 1 | 1 + 3 = 4 | No | false |
| 4 | 3 | 3 + 3 = 6 | Yes | true |

Returned result:

```text
[true, true, true, false, true]
```

## 6. Pattern Learned: Maximum Tracking + Array Traversal

### Maximum Tracking

Maintain a variable that stores the largest value encountered so far.

In this problem:

```cpp
if(candies[i]>max){
    max=candies[i];
}
```

### When is this pattern useful?

Look for maximum tracking when a problem asks you to:
- find the largest value in an array;
- compare each element against the array's maximum;
- make decisions based on the greatest value.

This problem uses two passes because we first need to know the overall maximum before checking each child's possible new total.

## 7. Time and Space Complexity

Let `n` be the number of children.

- **Time: O(n)** — the first loop finds the maximum and the second loop builds the answers. Each loop visits the array once.
- **Auxiliary space: O(n)** — the result vector stores one Boolean for every child. The extra working space apart from the required result is O(1).

## 8. Important Learning

1. A function's return type must match the type of value returned. `vector<int>` and `vector<bool>` are different types.
2. Use a separate result vector when the required output type differs from the input type.
3. `push_back()` appends an element to a vector.
4. Use `>=` when equality with the maximum should also qualify.
5. Finding a maximum first and then comparing every element against it is a useful two-pass array technique.
6. The input array is not modified.

## 9. Quick Revision

| Question | Answer |
|---|---|
| What does `max` store? | Greatest original candy count |
| Why use `vector<bool>`? | The required output is a Boolean for each child |
| Why use `result.push_back()`? | To append each child's true/false answer |
| Why use `>=`? | A child qualifies if the new total equals the maximum too |
| Does the code modify `candies`? | No |
| Pattern | Maximum Tracking + Two Array Traversals |
| Time complexity | O(n) |
| Auxiliary space including output | O(n) |
| Submission status | Accepted — 2026-11-02 |

**Core idea:** Find the current maximum first, then check whether each child's candies plus the extra candies can reach or exceed that maximum.
