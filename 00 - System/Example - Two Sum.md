---
pattern: "[[Arrays & Hashing]]"
difficulty: Easy
status: hint
date_solved: 2026-09-23
next_review: 2026-09-24
review_count: 0
leetcode: https://leetcode.com/problems/two-sum/
neetcode: https://neetcode.io/practice
tags: [problem, example]
---
# Two Sum

> [!example] This is an example note
> It shows how a finished problem note should look. Your own notes go in `02 - Problems/`: click a problem link in a pattern note (e.g. [[Two Sum]] in [[Arrays & Hashing]]) and insert the `Problem` template.

> [!key] Key Insight
> For each number, the partner I need is `target - num`. Store numbers I've **already seen** in a hashmap `value → index`, so each "does my partner exist?" check is O(1).

## Problem in my words
- **Input:** array `nums`, integer `target`
- **Output:** indices of the two numbers that add up to `target` (exactly one answer exists)
- **Constraints → target complexity:** n up to 10⁴, and the follow-up asks for better than O(n²), so aim for **O(n)**

## Triggers I should have noticed
- "find a **pair** that sums to X" in an **unsorted** array → hashmap of seen values
- (if it were **sorted** → [[Two Pointers]] instead, see Two Sum II)

## Brute force
- Idea: check every pair `(i, j)`
- Complexity: O(n²) time, O(1) space
- What's repeated / wasted: for each `i`, I re-scan the array looking for `target - nums[i]`. That scan is a **lookup**, and a hashmap does lookups in O(1).

## Optimal approach
1. Walk the array once.
2. For each `num`, compute `need = target - num`.
3. If `need` is in the map, return `[map[need], i]`. Otherwise store `map[num] = i`.

```python
def twoSum(nums: list[int], target: int) -> list[int]:
    seen = {}  # value -> index
    for i, num in enumerate(nums):
        need = target - num
        if need in seen:
            return [seen[need], i]
        seen[num] = i
    return []
```

- **Time:** O(n)
- **Space:** O(n)

## Where I got stuck / mistakes
- First tried to put everything in the map before looping. That breaks when `num == need` (same element used twice). Checking **before** inserting fixes it.

## Related
- [[Two Sum II Input Array Is Sorted]] (sorted → two pointers, O(1) space)
- [[3Sum]]

## Review log
| Date | Result | Notes |
|---|---|---|
| 2026-09-23 | first solve (hint) | needed the "check before insert" idea |
