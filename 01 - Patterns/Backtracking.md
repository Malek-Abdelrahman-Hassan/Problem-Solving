---
tags: [pattern]
phase: 2
order: 10
---
# Backtracking

> [!tip] In one line
> Build the answer one choice at a time: **choose → explore → un-choose**. It's a DFS over the tree of decisions.

## Recognize it
- "**all** subsets / combinations / permutations," "generate all," "return all possible"
- Placing things under constraints: N-Queens, Sudoku, word search in a grid
- Small `n` (≤ 15–20): exponential is expected

## Core idea
Draw the **decision tree** for a tiny input first. Every level is one decision. Then answer:
1. **What's my state?** (index `i`, current `path`)
2. **What are my choices at this state?**
3. **When do I record an answer / stop?**

## Templates
```python
# 1) Subsets: record at every node
res = []
def dfs(start, path):
    res.append(path[:])                  # copy!
    for i in range(start, len(nums)):
        path.append(nums[i])             # choose
        dfs(i + 1, path)                 # explore
        path.pop()                       # un-choose
dfs(0, [])

# 2) With duplicates in input: sort + skip
nums.sort()
def dfs(start, path):
    res.append(path[:])
    for i in range(start, len(nums)):
        if i > start and nums[i] == nums[i - 1]:
            continue
        path.append(nums[i])
        dfs(i + 1, path)
        path.pop()

# 3) Combination Sum (reuse allowed): recurse with i, not i + 1
def dfs(start, path, remaining):
    if remaining == 0:
        res.append(path[:]); return
    if remaining < 0:
        return
    for i in range(start, len(cands)):
        path.append(cands[i])
        dfs(i, path, remaining - cands[i])
        path.pop()

# 4) Permutations: track used
used = [False] * len(nums)
def dfs(path):
    if len(path) == len(nums):
        res.append(path[:]); return
    for i in range(len(nums)):
        if used[i]:
            continue
        used[i] = True; path.append(nums[i])
        dfs(path)
        used[i] = False; path.pop()

# 5) Grid (Word Search): mark visited, restore after
def dfs(r, c, i):
    if i == len(word):
        return True
    if not (0 <= r < R and 0 <= c < C) or board[r][c] != word[i]:
        return False
    tmp, board[r][c] = board[r][c], "#"
    found = any(dfs(r + dr, c + dc, i + 1) for dr, dc in ((1,0),(-1,0),(0,1),(0,-1)))
    board[r][c] = tmp
    return found
```

## Tricks to remember
- `i + 1` = each element used once. `i` = reuse allowed. `range(len)` + `used` = order matters (permutations).
- **N-Queens:** sets for `cols`, `r + c` (anti-diagonal), `r - c` (diagonal).
- **Palindrome Partitioning:** choice = where to cut next; only recurse if `s[start:end]` is a palindrome.
- **Letter Combinations:** one level per digit, choices = that digit's letters.

## Common mistakes
- `res.append(path)` instead of `path[:]`: every result ends up as the same (empty) list.
- Forgetting to undo (`pop`, reset `used`, restore the grid cell).
- Duplicate results: sort + `i > start` skip.

## Problems (NeetCode 150)
- [ ] [[Subsets]] (Medium)
- [ ] [[Combination Sum]] (Medium)
- [ ] [[Combination Sum II]] (Medium)
- [ ] [[Permutations]] (Medium)
- [ ] [[Subsets II]] (Medium)
- [ ] [[Word Search]] (Medium)
- [ ] [[Palindrome Partitioning]] (Medium)
- [ ] [[Letter Combinations of a Phone Number]] (Medium)
- [ ] [[N-Queens]] (Hard)

## My insights
- 

---
Prev: [[Heap - Priority Queue]] · Next: [[Graphs]] · [[Home]]
