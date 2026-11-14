---
tags: [pattern]
phase: 3
order: 14
---
# Greedy

> [!tip] In one line
> Make the **locally best choice** at each step and never look back. It works only when you can argue a local choice never ruins the global answer.

## Recognize it
- "maximum subarray" → Kadane
- "can you reach the end," "minimum jumps"
- A DP solution exists, but a single pass with a running best seems enough
- Sorting + taking items in order is natural (see also [[Intervals]])

## Core idea
Ask: *"What single value do I need to track as I sweep?"* (max reach, running sum, remaining gas…). Then: *"When do I reset it?"*

## Templates
```python
# 1) Kadane: maximum subarray
best, cur = nums[0], 0
for x in nums:
    cur = max(cur, 0) + x          # drop a negative prefix
    best = max(best, cur)

# 2) Jump Game: track the farthest reachable index
reach = 0
for i, jump in enumerate(nums):
    if i > reach:
        return False
    reach = max(reach, i + jump)
return True

# 3) Jump Game II: BFS by "levels" of reach
jumps, end, farthest = 0, 0, 0
for i in range(len(nums) - 1):
    farthest = max(farthest, i + nums[i])
    if i == end:                   # used up the current jump's range
        jumps += 1
        end = farthest
return jumps

# 4) Gas Station
if sum(gas) < sum(cost):
    return -1
tank, start = 0, 0
for i in range(len(gas)):
    tank += gas[i] - cost[i]
    if tank < 0:                   # can't start anywhere in [start, i]
        tank, start = 0, i + 1
return start
```

## Tricks to remember
- **Hand of Straights:** count map + min-heap (or sorted keys). Always start a group at the smallest remaining card.
- **Merge Triplets:** ignore any triplet with a value bigger than the target. Check that the good ones cover each target position.
- **Partition Labels:** record the last index of each char. Extend the current end, and cut when `i == end`.
- **Valid Parenthesis String:** track the range `[minOpen, maxOpen]`. `*` widens it. Clamp min at 0. Fail if max < 0.

## Common mistakes
- Using greedy without convincing yourself it's correct. Try to find a counter-example on a tiny input first.
- Kadane with all negative numbers: initialize `best = nums[0]`, not 0.

## Problems (NeetCode 150)
- [ ] [[Maximum Subarray]] (Medium)
- [ ] [[Jump Game]] (Medium)
- [ ] [[Jump Game II]] (Medium)
- [ ] [[Gas Station]] (Medium)
- [ ] [[Hand of Straights]] (Medium)
- [ ] [[Merge Triplets to Form Target Triplet]] (Medium)
- [ ] [[Partition Labels]] (Medium)
- [ ] [[Valid Parenthesis String]] (Medium)

## My insights
- 

---
Prev: [[2-D Dynamic Programming]] · Next: [[Intervals]] · [[Home]]
