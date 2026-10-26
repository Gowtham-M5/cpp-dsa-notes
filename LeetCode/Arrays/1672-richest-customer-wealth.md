# LeetCode 1672 — Richest Customer Wealth

## Problem
Each row in `accounts` contains one customer's bank balances. Return the maximum total wealth of any customer.

## Core idea: Sum each row separately
- Start with a maximum wealth value of `0`.
- For each customer (row), reset the row's sum to `0`.
- Add every balance in that row.
- Compare the row total with the maximum wealth and keep the larger value.
- After checking all customers, return the maximum wealth.

## Important concept
Reset the sum for every customer. If the sum is not reset for each row, balances from different customers will be mixed together.

## Code note
The code previously saved here was not verified as the exact code I personally wrote. It has been removed rather than presenting an assistant-written implementation as mine. Add my own code after retrying the problem.

## Complexity
If there are `r` customers and `c` accounts per customer:
- Time: `O(r × c)`
- Extra space: `O(1)`
