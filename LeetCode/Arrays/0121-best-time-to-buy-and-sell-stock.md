# LeetCode 121 — Best Time to Buy and Sell Stock

## Problem
Choose one day to buy and a later day to sell. Return the maximum profit; return `0` if no profit is possible.

## Core idea: Track the minimum price so far
- `minprice`: lowest price seen so far.
- `maxprofit`: best profit found so far.
- For each price, calculate today's profit using the minimum buying price, update the best profit, then update the minimum price for future days.

## C++ solution
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxprofit = 0;
        int minprice = prices[0];

        for (int i = 1; i < prices.size(); i++) {
            int profit = prices[i] - minprice;
            if (profit > maxprofit) {
                maxprofit = profit;
            }

            if (prices[i] < minprice) {
                minprice = prices[i];
            }
        }

        return maxprofit;
    }
};
```

## Trace
For `prices = [7,1,5,3,6,4]`:

| Current price | Profit using minimum so far | Best profit | Minimum after processing |
|---:|---:|---:|---:|
| 1 | 1 - 7 = -6 | 0 | 1 |
| 5 | 5 - 1 = 4 | 4 | 1 |
| 3 | 3 - 1 = 2 | 4 | 1 |
| 6 | 6 - 1 = 5 | 5 | 1 |
| 4 | 4 - 1 = 3 | 5 | 1 |

Answer: `5` (buy at 1, sell at 6).

## Why update minimum price?
Today's lower price could be a better buying point for a later day. We calculate today's profit first, then store the lower price for future comparisons.

## Pattern
Track the best candidate seen so far while scanning the array once.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
