---
tags: [pattern]
phase: 1
order: 3
---
# Sliding Window

> [!tip] In one line
> A **contiguous** range `[left, right]` that grows on the right and shrinks on the left, so each element enters and leaves once: O(n).

## Recognize it
- "**contiguous** subarray / substring"
- "longest / shortest / maximum / minimum" + a condition ("without repeating," "at most K changes," "contains all of")
- "window of size k"
- Brute force re-scans overlapping ranges

## Core idea
Keep some **state** about the window (a counter, a sum, a set). Expand `right` every step. While the window is **invalid**, shrink from `left`. Update the answer when it's valid.

## Templates
```python
# 1) Variable window: LONGEST valid
def longest(s):
    count = {}
    left = best = 0
    for right, ch in enumerate(s):
        count[ch] = count.get(ch, 0) + 1          # add right
        while invalid(count, left, right):         # shrink until valid
            count[s[left]] -= 1
            left += 1
        best = max(best, right - left + 1)         # window is valid here
    return best

# 2) Variable window: SHORTEST valid
def shortest(nums, target):
    left, total, best = 0, 0, float("inf")
    for right, x in enumerate(nums):
        total += x
        while total >= target:                     # shrink while STILL valid
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1
    return best if best != float("inf") else 0

# 3) Fixed window of size k
window = sum(nums[:k])
best = window
for right in range(k, len(nums)):
    window += nums[right] - nums[right - k]
    best = max(best, window)
```

```python
# 4) Max of every window: monotonic deque of indices (values decreasing)
from collections import deque
q, res = deque(), []
for r, x in enumerate(nums):
    while q and nums[q[-1]] < x:
        q.pop()
    q.append(r)
    if q[0] <= r - k:          # front fell out of the window
        q.popleft()
    if r >= k - 1:
        res.append(nums[q[0]])
```

## Tricks to remember
- **Longest Repeating Character Replacement:** window valid if `length - maxFreq <= k`.
- **Permutation in String / Min Window Substring:** compare counts using a `matches` / `have == need` counter instead of comparing whole dicts every step.
- **Best Time to Buy and Sell Stock:** left = cheapest day so far; move it when you find a cheaper price.
- Longest window: update answer **after** shrinking. Shortest window: update **while** shrinking.

## Common mistakes
- Using a window on non-contiguous problems (subsequence ≠ substring).
- Negative numbers break sum-based windows. Use prefix sums + hashmap instead.
- Off-by-one: window length is `right - left + 1`.

## Problems (NeetCode 150)
- [ ] [[Best Time to Buy and Sell Stock]] (Easy)
- [ ] [[Longest Substring Without Repeating Characters]] (Medium)
- [ ] [[Longest Repeating Character Replacement]] (Medium)
- [ ] [[Permutation in String]] (Medium)
- [ ] [[Minimum Window Substring]] (Hard)
- [ ] [[Sliding Window Maximum]] (Hard)

## My insights
- 

---
Prev: [[Two Pointers]] · Next: [[Stack]] · [[Home]]
