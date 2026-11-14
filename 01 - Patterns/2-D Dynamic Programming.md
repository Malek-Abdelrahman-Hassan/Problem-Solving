---
tags: [pattern]
phase: 3
order: 13
---
# 2-D Dynamic Programming

> [!tip] In one line
> Same 4 steps as [[1-D Dynamic Programming]], but the state needs **two numbers**: a grid cell `(r, c)`, two string positions `(i, j)`, or `(index, remaining amount)`.

## Recognize it
- **Two strings** compared: common subsequence, edit distance, interleaving, regex matching
- A **grid** with moves right/down: "unique paths," "min path sum"
- A choice problem with **index + capacity** ("coin change II," "target sum," knapsack)
- Stock problems with a **state machine** (holding / not holding / cooldown)

## Core idea
`dp[i][j]` usually means **"answer for suffixes `a[i:]` and `b[j:]`"** (or prefixes). Look at the **first characters** and list the choices.

## Templates
```python
from functools import cache

# 1) Two strings: Longest Common Subsequence (top-down)
def lcs(a, b):
    @cache
    def dp(i, j):
        if i == len(a) or j == len(b):
            return 0
        if a[i] == b[j]:
            return 1 + dp(i + 1, j + 1)
        return max(dp(i + 1, j), dp(i, j + 1))
    return dp(0, 0)

# 2) Same, bottom-up table (fill from the end)
def lcs(a, b):
    dp = [[0] * (len(b) + 1) for _ in range(len(a) + 1)]
    for i in range(len(a) - 1, -1, -1):
        for j in range(len(b) - 1, -1, -1):
            if a[i] == b[j]:
                dp[i][j] = 1 + dp[i + 1][j + 1]
            else:
                dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])
    return dp[0][0]

# 3) Grid paths (one row is enough)
row = [1] * n
for _ in range(m - 1):
    for c in range(1, n):
        row[c] += row[c - 1]            # from above (row[c]) + from left
return row[-1]

# 4) Count ways with unlimited items: Coin Change II
dp = [1] + [0] * amount
for coin in coins:                      # coins OUTER → combinations, not permutations
    for a in range(coin, amount + 1):
        dp[a] += dp[a - coin]
return dp[amount]
```

## Recurrences worth memorizing
| Problem | Recurrence (on suffixes i, j) |
|---|---|
| Edit Distance | equal → `dp[i+1][j+1]`; else `1 + min(insert dp[i][j+1], delete dp[i+1][j], replace dp[i+1][j+1])` |
| Distinct Subsequences | `dp[i+1][j]` + (`dp[i+1][j+1]` if `s[i]==t[j]`) |
| Interleaving String | `dp[i][j]` true if (`s1[i]` matches `s3[i+j]` and `dp[i+1][j]`) or (same for `s2`) |
| Target Sum | memo on `(i, current_sum)`: add or subtract `nums[i]` |
| Stock with Cooldown | states `(i, holding)`: buy → `i+1`, sell → `i+2` (cooldown) |
| Longest Increasing Path in Matrix | DFS + memo on `(r, c)`; no visited set needed (strictly increasing) |
| Burst Balloons | interval DP: pick the **last** balloon to burst in `(l, r)` |

## Common mistakes
- Table size off by one: suffix DP needs `(len + 1)` rows/cols for the empty base case.
- Coin Change II: loops in the wrong order count permutations instead of combinations.
- Jumping straight to a table. Write the memoized recursion first; it's much easier to get right.

## Problems (NeetCode 150)
- [ ] [[Unique Paths]] (Medium)
- [ ] [[Longest Common Subsequence]] (Medium)
- [ ] [[Best Time to Buy and Sell Stock With Cooldown]] (Medium)
- [ ] [[Coin Change II]] (Medium)
- [ ] [[Target Sum]] (Medium)
- [ ] [[Interleaving String]] (Medium)
- [ ] [[Longest Increasing Path in a Matrix]] (Hard)
- [ ] [[Distinct Subsequences]] (Hard)
- [ ] [[Edit Distance]] (Medium)
- [ ] [[Burst Balloons]] (Hard)
- [ ] [[Regular Expression Matching]] (Hard)

## My insights
- 

---
Prev: [[1-D Dynamic Programming]] · Next: [[Greedy]] · [[Home]]
