---
tags: [pattern]
phase: 1
order: 5
---
# Binary Search

> [!tip] In one line
> If you can answer "is the target **left or right** of mid?", you can discard half the search space each step: O(log n).

## Recognize it
- Input is **sorted** (or sorted-then-rotated)
- "Find in O(log n)"
- "**Minimum** X such that…" / "**maximum** X such that…", with a huge answer range (this is binary search **on the answer**)
- A condition that's monotonic: false false false **true true true**

## Core idea
Binary search isn't really about arrays. It works on any **monotonic yes/no function**: find the first `true`.

## Templates
```python
# 1) Classic: find exact target
l, r = 0, len(nums) - 1
while l <= r:
    m = (l + r) // 2
    if nums[m] == target:
        return m
    if nums[m] < target:
        l = m + 1
    else:
        r = m - 1
return -1

# 2) First TRUE (lower bound / binary search on answer)
def first_true(lo, hi):          # answer is in [lo, hi]
    while lo < hi:
        m = (lo + hi) // 2
        if feasible(m):
            hi = m               # m might be the answer, keep it
        else:
            lo = m + 1           # m is too small
    return lo

# Koko: feasible(k) = sum(ceil(p / k) for p in piles) <= h, range [1, max(piles)]
```

```python
# 3) Rotated sorted array: one half is always sorted
l, r = 0, len(nums) - 1
while l <= r:
    m = (l + r) // 2
    if nums[m] == target:
        return m
    if nums[l] <= nums[m]:                   # left half sorted
        if nums[l] <= target < nums[m]:
            r = m - 1
        else:
            l = m + 1
    else:                                    # right half sorted
        if nums[m] < target <= nums[r]:
            l = m + 1
        else:
            r = m - 1
```

## Tricks to remember
- **Search a 2D Matrix:** treat it as one sorted array: `row, col = divmod(mid, cols)`.
- **Find Min in Rotated:** compare `nums[m]` with `nums[r]`. If bigger, the min is to the right.
- **Time Based Key-Value Store:** timestamps come in sorted, so binary search for the largest `<= t`.
- **Median of Two Sorted Arrays:** binary search the **partition** of the smaller array.

## Common mistakes
- Infinite loop: with `while lo < hi` you must use `hi = m` and `lo = m + 1` (never `lo = m`).
- Mixing templates: `l <= r` goes with `r = m - 1`; `l < r` goes with `r = m`.
- Wrong search range in "binary search on answer." Write down the min and max possible answers first.

## Problems (NeetCode 150)
- [ ] [[Binary Search (Problem)|Binary Search]] (Easy)
- [ ] [[Search a 2D Matrix]] (Medium)
- [ ] [[Koko Eating Bananas]] (Medium)
- [ ] [[Find Minimum in Rotated Sorted Array]] (Medium)
- [ ] [[Search in Rotated Sorted Array]] (Medium)
- [ ] [[Time Based Key-Value Store]] (Medium)
- [ ] [[Median of Two Sorted Arrays]] (Hard)

> [!note] Naming
> The LeetCode problem "Binary Search" has the same name as this note. Name its problem note `Binary Search (Problem)` to avoid a clash.

## My insights
- 

---
Prev: [[Stack]] · Next: [[Linked List]] · [[Home]]
