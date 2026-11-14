---
tags: [pattern]
phase: 3
order: 15
---
# Intervals

> [!tip] In one line
> **Sort first.** Once intervals are sorted by start, each one only needs to be compared with the **last** one you kept.

## Recognize it
- Input is a list of `[start, end]` pairs
- "merge," "insert," "overlapping," "meetings," "rooms," "remove minimum to make non-overlapping"

## Core idea
Two intervals `[a, b]` and `[c, d]` (with `a <= c`) overlap iff `c <= b`.
- Merging / inserting → **sort by start**
- Keep the maximum number of non-overlapping intervals → **sort by end** (greedy)
- Count simultaneous overlaps (rooms) → **min-heap of end times** or a **sweep line**

## Templates
```python
# 1) Merge intervals
intervals.sort(key=lambda x: x[0])
merged = [intervals[0]]
for start, end in intervals[1:]:
    if start <= merged[-1][1]:                 # overlap
        merged[-1][1] = max(merged[-1][1], end)
    else:
        merged.append([start, end])

# 2) Non-overlapping: min removals (sort by END)
intervals.sort(key=lambda x: x[1])
removed, prev_end = 0, float("-inf")
for start, end in intervals:
    if start >= prev_end:
        prev_end = end                          # keep it
    else:
        removed += 1                            # drop it (it ends later)

# 3) Meeting Rooms II: min-heap of end times
import heapq
intervals.sort(key=lambda x: x[0])
ends = []
for start, end in intervals:
    if ends and ends[0] <= start:
        heapq.heappop(ends)                     # reuse the room that freed up
    heapq.heappush(ends, end)
return len(ends)
```

## Tricks to remember
- **Insert Interval:** three phases: add all intervals ending before the new one, merge the overlapping ones, add the rest. No sort needed (the input is sorted).
- **Meeting Rooms (I):** sort, then check `intervals[i][0] < intervals[i-1][1]`.
- **Min Interval to Include Each Query:** sort intervals and queries. Push intervals starting ≤ query into a heap keyed by size, pop the ones that already ended.

## Common mistakes
- Forgetting to sort.
- `<` vs `<=` for touching intervals (`[1,2]` and `[2,3]`): read the problem carefully.
- Mutating the input when the problem expects a new list (usually fine on LeetCode).

## Problems (NeetCode 150)
- [ ] [[Insert Interval]] (Medium)
- [ ] [[Merge Intervals]] (Medium)
- [ ] [[Non-overlapping Intervals]] (Medium)
- [ ] [[Meeting Rooms]] (Easy)
- [ ] [[Meeting Rooms II]] (Medium)
- [ ] [[Minimum Interval to Include Each Query]] (Hard)

## My insights
- 

---
Prev: [[Greedy]] · Next: [[Advanced Graphs]] · [[Home]]
