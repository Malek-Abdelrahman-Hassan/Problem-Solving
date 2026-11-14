---
tags: [pattern]
phase: 1
order: 1
---
# Arrays & Hashing

> [!tip] In one line
> Trade memory for speed: store what you've seen in a **set / hashmap** so every "have I seen this?" check is O(1) instead of O(n).

## Recognize it
- "contains duplicate," "count," "frequency," "anagram," "group by"
- A brute force with a nested loop whose inner loop is **searching** for something
- "find pair with sum X" in an **unsorted** array
- "subarray sum equals K" (prefix sums + hashmap)

## Core idea
Ask: *"What am I searching for repeatedly?"* Put that in a hashmap keyed by what you'll look up.

## Templates
```python
from collections import Counter, defaultdict

# 1) Seen set: duplicates
seen = set()
for x in nums:
    if x in seen:
        return True
    seen.add(x)

# 2) Frequency count
count = Counter(s)            # or: count[c] = count.get(c, 0) + 1

# 3) Complement lookup: pair with sum
idx = {}
for i, x in enumerate(nums):
    if target - x in idx:
        return [idx[target - x], i]
    idx[x] = i

# 4) Group by a canonical key
groups = defaultdict(list)
for w in words:
    groups[tuple(sorted(w))].append(w)   # or a 26-count tuple

# 5) Prefix sum + hashmap: count subarrays summing to k
count, prefix, freq = 0, 0, {0: 1}
for x in nums:
    prefix += x
    count += freq.get(prefix - k, 0)
    freq[prefix] = freq.get(prefix, 0) + 1
```

## Tricks to remember
- **Bucket sort** for top-K frequency: index = frequency, O(n).
- **Prefix & suffix products** (Product Except Self): two passes, no division.
- **Longest consecutive:** only start counting from `x` when `x - 1` isn't in the set.
- **Canonical key:** sorted string, or a tuple of 26 counts, groups anagrams.

## Common mistakes
- Using a `list` for membership checks (O(n)) instead of a `set`.
- Inserting before checking (Two Sum: the element pairs with itself).
- Using a mutable `list` as a dict key. Use a `tuple`.

## Problems (NeetCode 150)
- [x] [[Contains Duplicate]] (Easy)
- [x] [[Valid Anagram]] (Easy)
- [x] [[Two Sum]] (Easy)
- [ ] [[Group Anagrams]] (Medium)
- [ ] [[Top K Frequent Elements]] (Medium)
- [ ] [[Encode and Decode Strings]] (Medium)
- [ ] [[Product of Array Except Self]] (Medium)
- [ ] [[Valid Sudoku]] (Medium)
- [ ] [[Longest Consecutive Sequence]] (Medium)

## My insights
- 

---
Next: [[Two Pointers]] · [[Home]]
