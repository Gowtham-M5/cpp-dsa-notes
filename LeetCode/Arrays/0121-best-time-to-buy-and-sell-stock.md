# LeetCode #121: Best Time to Buy and Sell Stock

**Topic:** Arrays  
**Difficulty:** Easy  
**Pattern:** Track the Minimum So Far  
**Status:** Optimized solution understood

## 1. Problem Statement

Given an array `prices`, where `prices[i]` represents the stock price on day `i`, find the maximum profit you can achieve.

- You can buy the stock only once.
- You must sell it on a later day than you bought it.
- If no profitable transaction is possible, return `0`.

**Example:**

```cpp
prices = [7, 1, 5, 3, 6, 4]
Output: 5
```

Buy at `1` and sell at `6`. Maximum profit = `6 - 1 = 5`.

## 2. Approach 1: Brute Force

### Logic
Use two loops to check every valid buying and selling combination.

- Outer loop: Select the selling day.
- Inner loop: Check all previous days as buying days.
- Calculate `selling price - buying price`.
- Update the maximum profit.

### Code
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxprofit = 0;

        for (int i = prices.size() - 1; i >= 0; i--) {
            for (int j = i - 1; j >= 0; j--) {
                if (prices[i] - prices[j] > maxprofit) {
                    maxprofit = prices[i] - prices[j];
                }
            }
        }

        return maxprofit;
    }
};
```

**Time Complexity:** `O(n²)`  
**Space Complexity:** `O(1)`

This approach can cause Time Limit Exceeded for large inputs because it checks too many combinations.

## 3. Approach 2: Optimized Single Loop

### Key Idea
Instead of checking every previous day, remember the minimum price encountered so far.

```cpp
int minprice = prices[0];
int maxprofit = 0;
```

- `minprice`: Lowest stock price encountered so far.
- `maxprofit`: Highest profit found so far.

For each new price:
1. Calculate today's potential profit using the previous minimum price.
2. Update `maxprofit` if today's profit is greater.
3. Update `minprice` if today's price is lower.

### Optimized C++ Solution
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxprofit = 0;
        int minprice = prices[0];

        for (int i = 1; i < prices.size(); i++) {
            if (prices[i] - minprice > maxprofit) {
                maxprofit = prices[i] - minprice;
            }

            minprice = min(minprice, prices[i]);
        }

        return maxprofit;
    }
};
```

## 4. Dry Run

Input: `prices = [7, 1, 5, 3, 6, 4]`

Initially: `minprice = 7`, `maxprofit = 0`.

| Day | Today's Price | Minimum Before Today | Potential Profit | Maximum Profit | Minimum After Today |
| --- | ------------- | -------------------- | ---------------- | -------------- | ------------------- |
| 1 | 7 | — | — | 0 | 7 |
| 2 | 1 | 7 | -6 | 0 | 1 |
| 3 | 5 | 1 | 4 | 4 | 1 |
| 4 | 3 | 1 | 2 | 4 | 1 |
| 5 | 6 | 1 | 5 | 5 | 1 |
| 6 | 4 | 1 | 3 | 5 | 1 |

Final answer: `5`. Buy at `1` and sell at `6`.

## 5. Why Calculate Profit Before Updating the Minimum?

Consider `prices = [8, 3, 6]`.

When we reach price `6`, `minprice = 3`. Calculate profit: `6 - 3 = 3`, then update `maxprofit = 3`, and finally update the minimum:

```cpp
minprice = min(3, 6);  // 3
```

Calculating profit first ensures the minimum price represents an earlier day. Updating the minimum first would not change the final answer for this particular problem, but calculating profit first makes the buy-before-sell logic explicit.

## 6. Important Edge Cases

### Prices keep decreasing
`prices = [9, 7, 4, 2]` → output: `0`. No profitable transaction is possible.

### Only one price
`prices = [5]` → output: `0`. The loop does not execute, and the function returns `0`.

### Increasing prices
`prices = [1, 2, 3, 4, 5]` → output: `4`. Buy at `1` and sell at `5`.

### Minimum price occurs on the last day
`prices = [7, 6, 4, 3, 1]` → output: `0`. You cannot buy at `1` and sell afterward.

## 7. Complexity Analysis

| Approach | Time Complexity | Space Complexity |
| --- | --- | --- |
| Brute force | `O(n²)` | `O(1)` |
| Optimized | `O(n)` | `O(1)` |

The optimized solution traverses the array once and uses two variables.

## 8. Pattern to Remember

**Pattern: Track the Minimum So Far + Maximum Result So Far**

Useful when you need to find the best result while traversing an array, can maintain useful information from previous elements, and want to avoid checking every possible pair.

Core logic:
```cpp
calculate current result;
update best result;
update minimum so far;
```

## 9. Learning Progression

1. Started with brute force using two loops.
2. Understood why brute force can cause TLE.
3. Identified the minimum-price tracking approach.
4. Optimized the solution to `O(n)`.
5. Practiced dry runs and edge cases.
