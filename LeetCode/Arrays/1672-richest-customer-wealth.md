# LeetCode 1672 — Richest Customer Wealth

## Problem
Each row in `accounts` contains one customer's bank balances. Return the maximum total wealth of any customer.

## Core idea: Sum each row separately
- Set `maxWealth = 0).
- For each customer (row), reset `sum = 0).
- Add all balances in that row.
- Compare the row's total with `maxWealth` and keep the larger value.

## C++ solution
```cpp
class Solution {
public:
    int maximumWealth(vector<vector<int>>& accounts) {
        int maxWealth = 0;

        for (int i = 0; i < accounts.size(); i++) {
            int sum = 0;

            for (int j = 0; j < accounts[i].size(); j++) {
                sum += accounts[i][j];
            }

            if (sum > maxWealth) {
                maxWealth = sum;
            }
        }

        return maxWealth;
    }
};
```

## Common mistake
Reset `sum = 0` for every customer. If it is declared outside the outer loop and not reset, balances from different customers will be mixed together.

## Complexity
If there are `r` customers and `c` accounts per customer:
- Time: `O(r × c)`
- Extra space: `O(1)`
