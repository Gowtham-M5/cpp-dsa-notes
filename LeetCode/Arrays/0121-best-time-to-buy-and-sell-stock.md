# LeetCode 121 — Best Time to Buy and Sell Stock

## Problem
Choose one day to buy and a later day to sell. Return the maximum profit; return `0` if no profit is possible.

## Core idea: Track the minimum price so far
- `minprice`: lowest price seen so far.
- `maxprofit`: best profit found so far.
- For each later price, calculate the profit using the minimum buying price seen before that day.
- Update the best profit when today's profit is larger.
- Update the minimum price when today's price is lower.

The order matters: calculate the profit using the minimum price from earlier days, then update the minimum price for future days.

## Example
For `prices = [7,1,5,3,6,4]`:
- Buy at `1`, then sell later at `5`: profit `4`.
- Sell later at `6`: profit `5`, which becomes the best profit.
- The maximum profit is `5`.

For `prices = [7,6,4,3,1]`, prices keep decreasing, so the answer is `0`.

## Code note
The code previously saved here was not verified as the exact code I personally wrote. It has been removed rather than presenting an assistant-written implementation as mine. Add my own code after I retry the problem.

## Complexity
- Time: `O(n)`
- Extra space: `O(1)`
