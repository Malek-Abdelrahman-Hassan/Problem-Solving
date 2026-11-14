---
tags: [pattern]
phase: 3
order: 12
---
# 1-D Dynamic Programming

> [!tip] In one line
> DP = **recursion + memory**. If your brute-force recursion solves the same subproblem again and again, cache it.

## Recognize it
- "**number of ways**," "**minimum / maximum** cost / sum / length," "**can you** reach / make / break"
- At each step you make a **choice** (take / skip, 1 step / 2 steps, which coin)
- The answer for `i` depends on answers for smaller `i`
- Brute force is exponential [[Backtracking]] that recomputes the same states

## Core idea: the 4 steps (write them BEFORE coding)
1. **State:** `dp[i]` = *(write the exact meaning in words)*, e.g. "max money robbing houses `0..i`"
2. **Recurrence:** how `dp[i]` comes from smaller states (list the choices!)
3. **Base cases:** the smallest `i` values
4. **Order & answer:** fill from small to large; where's the answer? (`dp[n]`? `max(dp)`?)

> [!important] Path to learn DP
> **Brute-force recursion → add memo (top-down) → convert to a table (bottom-up) → shrink to 2 variables.**
> Always start with the recursion. The table version is just the same recursion filled in order.

## Templates
```python
from functools import cache

# 1) Top-down: write the recursion, add @cache
def rob(nums):
    @cache
    def dp(i):                          # max money from houses i..end
        if i >= len(nums):
            return 0
        return max(dp(i + 1),           # skip house i
                   nums[i] + dp(i + 2)) # rob house i
    return dp(0)

# 2) Bottom-up with two variables
def rob(nums):
    prev2, prev1 = 0, 0                 # dp[i-2], dp[i-1]
    for x in nums:
        prev2, prev1 = prev1, max(prev1, prev2 + x)
    return prev1

# 3) Unbounded choices: Coin Change (min coins)
dp = [0] + [float("inf")] * amount
for a in range(1, amount + 1):
    for coin in coins:
        if coin <= a:
            dp[a] = min(dp[a], dp[a - coin] + 1)
return dp[amount] if dp[amount] != float("inf") else -1

# 4) "Can we split" DP: Word Break
dp = [False] * (len(s) + 1)
dp[len(s)] = True                       # empty suffix is breakable
for i in range(len(s) - 1, -1, -1):
    for w in wordDict:
        if s.startswith(w, i) and dp[i + len(w)]:
            dp[i] = True
            break
return dp[0]
```

## Recurrences worth memorizing
| Problem | Recurrence |
|---|---|
| Climbing Stairs | `dp[i] = dp[i-1] + dp[i-2]` |
| House Robber | `dp[i] = max(dp[i-1], dp[i-2] + nums[i])` |
| House Robber II | circle → `max(rob(nums[1:]), rob(nums[:-1]))` |
| Decode Ways | `dp[i] = dp[i+1] (if s[i] != '0') + dp[i+2] (if s[i:i+2] in 10..26)` |
| Max Product Subarray | track **both** `curMax` and `curMin` (negative × negative) |
| LIS (O(n²)) | `dp[i] = 1 + max(dp[j] for j > i if nums[j] > nums[i])` |
| Partition Equal Subset | set of reachable sums; target = `total / 2` |
| Palindromic substrings | **expand around center** (odd and even), not a table |

## Common mistakes
- Coding before defining the state in words.
- Wrong base case (e.g. `dp[0]` for Coin Change is 0, not 1).
- Forgetting that the answer might be `max(dp)`, not `dp[-1]` (LIS).

## Problems (NeetCode 150)
- [ ] [[Climbing Stairs]] (Easy)
- [ ] [[Min Cost Climbing Stairs]] (Easy)
- [ ] [[House Robber]] (Medium)
- [ ] [[House Robber II]] (Medium)
- [ ] [[Longest Palindromic Substring]] (Medium)
- [ ] [[Palindromic Substrings]] (Medium)
- [ ] [[Decode Ways]] (Medium)
- [ ] [[Coin Change]] (Medium)
- [ ] [[Maximum Product Subarray]] (Medium)
- [ ] [[Word Break]] (Medium)
- [ ] [[Longest Increasing Subsequence]] (Medium)
- [ ] [[Partition Equal Subset Sum]] (Medium)

## My insights
- 

---
Prev: [[Graphs]] · Next: [[2-D Dynamic Programming]] · [[Home]]
