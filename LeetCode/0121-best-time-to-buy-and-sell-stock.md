# LeetCode 121 — Best Time to Buy and Sell Stock

## Problem
Given daily stock prices, choose one day to buy and a later day to sell. Return the maximum possible profit. If no profit is possible, return `0`.

## Key idea: Track the minimum price so far
- `minprice` stores the lowest price seen up to the current day.
- `maxprofit` stores the best profit found so far.
- For each new price, calculate the profit from buying at `minprice` and selling today.
- Update `maxprofit` if this profit is better.
- Then update `minprice` if today's price is lower.

## C++ solution
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

| Current price | Minimum so far used for profit | Profit today | Best profit | Minimum after processing |
|---:|---:|---:|---:|---:|
| 1 | 7 | -6 | 0 | 1 |
| 5 | 1 | 4 | 4 | 1 |
| 3 | 1 | 2 | 4 | 1 |
| 6 | 1 | 5 | 5 | 1 |
| 4 | 1 | 3 | 5 | 1 |

Answer: `5` (buy at 1, sell at 6).

## Why update the minimum price too?
A lower price today may make a better buying point for a future day. We still calculate today's possible profit using the minimum seen before or up to today, then keep the lowest price for future comparisons. Updating the minimum after the profit check makes the sequence especially easy to reason about.

## Important pattern
**Track the best candidate seen so far while scanning once.** Here, the candidate is the minimum buying price.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
