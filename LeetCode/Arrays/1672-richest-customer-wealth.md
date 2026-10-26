# LeetCode 1672 — Richest Customer Wealth

## Problem
Each row in `accounts` contains one customer's bank balances. Return the maximum total wealth of any customer.

## Core idea: Sum each row separately
- Start `maxwealth` at `0`.
- For every customer, reset `sum` to `0`.
- Add all balances in that row.
- If the row sum is greater than `maxwealth`, update `maxwealth`.
- Return `maxwealth`.

## Code from my practiced solution
```cpp
class Solution {
public:
    int maximumWealth(vector<vector<int>>& accounts) {
        int maxwealth = 0;
        for (int i = 0; i < accounts.size(); i++) {
            int sum = 0;
            for (int j = 0; j < accounts[i].size(); j++) {
                sum += accounts[i][j];
            }
            if (sum > maxwealth) {
                maxwealth = sum;
            }
        }
        return maxwealth;
    }
};
```

## Important concept
Reset `sum = 0` for every customer. Otherwise, balances from different customers would be added together.

## Complexity
If there are `r` customers and `c` accounts per customer:
- Time: `O(r × c)`
- Extra space: `O(1)`
