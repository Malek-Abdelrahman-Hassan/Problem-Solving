---
tags: [pattern]
phase: 2
order: 9
aliases: [Heap, Priority Queue]
---
# Heap / Priority Queue

> [!tip] In one line
> Get the smallest (or largest) item in O(log n) while items keep arriving. Perfect for "**top K**," "**K-th**," and "**always process the best next**."

## Recognize it
- "K largest / smallest / closest / most frequent"
- "K-th largest" (especially in a stream)
- "median of a stream" → two heaps
- Repeatedly take the max/min, change it, put it back (Last Stone Weight, Task Scheduler)
- Merging K sorted things

## Core idea
Python's `heapq` is a **min-heap**. For a max-heap, push negated values.
**Top K largest → keep a MIN-heap of size K.** The smallest of the top K sits on top and gets kicked out first.

## Templates
```python
import heapq

# 1) Min-heap basics
h = []
heapq.heappush(h, x)
smallest = heapq.heappop(h)
top = h[0]                         # peek
heapq.heapify(nums)                # O(n) in place

# 2) Max-heap: negate
heapq.heappush(h, -x)
largest = -heapq.heappop(h)

# 3) K largest: min-heap of size k
h = []
for x in nums:
    heapq.heappush(h, x)
    if len(h) > k:
        heapq.heappop(h)
return h[0]                        # k-th largest

# 4) Two heaps: running median
small, large = [], []              # small = max-heap (negated), large = min-heap
def add(num):
    heapq.heappush(small, -num)
    heapq.heappush(large, -heapq.heappop(small))   # move small's max to large
    if len(large) > len(small):
        heapq.heappush(small, -heapq.heappop(large))
def median():
    if len(small) > len(large):
        return -small[0]
    return (-small[0] + large[0]) / 2
```

## Tricks to remember
- Push **tuples** `(priority, tiebreak, item)`. Python compares tuples element by element.
- **K Closest Points:** max-heap of size k on `-(x² + y²)`, or `heapq.nsmallest(k, points, key=...)`.
- **Task Scheduler:** max-heap of counts + a queue of `(count, ready_time)` for cooldown. There's also a math formula: `(maxCount - 1) * (n + 1) + numWithMaxCount`, then take the max with `len(tasks)`.
- **Design Twitter:** merge K users' tweet lists with a heap (like Merge K Sorted Lists).

## Common mistakes
- Using a max-heap of all n items for top-K: O(n log n) instead of O(n log k).
- Forgetting to negate back when popping from a "max-heap."
- Pushing objects that can't be compared (add an index as tiebreaker).

## Problems (NeetCode 150)
- [ ] [[Kth Largest Element in a Stream]] (Easy)
- [ ] [[Last Stone Weight]] (Easy)
- [ ] [[K Closest Points to Origin]] (Medium)
- [ ] [[Kth Largest Element in an Array]] (Medium)
- [ ] [[Task Scheduler]] (Medium)
- [ ] [[Design Twitter]] (Medium)
- [ ] [[Find Median From Data Stream]] (Hard)

## My insights
- 

---
Prev: [[Tries]] · Next: [[Backtracking]] · [[Home]]
