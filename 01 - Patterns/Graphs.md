---
tags: [pattern]
phase: 2
order: 11
---
# Graphs

> [!tip] In one line
> Nodes + edges. Almost everything is **DFS/BFS with a visited set**, plus two specials: **topological sort** (dependencies) and **Union-Find** (components).

## Recognize it
- 2D grid of cells ("islands," "regions," "rotting," "flood fill"). Each cell is a node with 4 neighbors.
- Explicit edges / adjacency list
- "shortest / minimum steps," unweighted → **BFS**
- "spreads from all sources at the same time" → **multi-source BFS**
- "prerequisites," "order," "can you finish" → **topological sort**
- "connected components," "redundant connection," "valid tree" → **Union-Find**

## Core idea
1. Build the graph (adjacency list), or treat the grid as the graph.
2. Pick the traversal: DFS (explore / count / mark) or BFS (distance / levels).
3. **Mark visited when you push**, never revisit.

## Templates
```python
from collections import deque, defaultdict

DIRS = ((1, 0), (-1, 0), (0, 1), (0, -1))

# 1) Grid DFS: count islands
def numIslands(grid):
    R, C = len(grid), len(grid[0])
    def dfs(r, c):
        if not (0 <= r < R and 0 <= c < C) or grid[r][c] != "1":
            return
        grid[r][c] = "0"                    # mark visited
        for dr, dc in DIRS:
            dfs(r + dr, c + dc)
    count = 0
    for r in range(R):
        for c in range(C):
            if grid[r][c] == "1":
                dfs(r, c)
                count += 1
    return count

# 2) Multi-source BFS (Rotting Oranges, Walls and Gates)
q = deque((r, c) for r in range(R) for c in range(C) if grid[r][c] == 2)
fresh = sum(row.count(1) for row in grid)
minutes = 0
while q and fresh:
    for _ in range(len(q)):                 # one "minute" = one level
        r, c = q.popleft()
        for dr, dc in DIRS:
            nr, nc = r + dr, c + dc
            if 0 <= nr < R and 0 <= nc < C and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                fresh -= 1
                q.append((nr, nc))
    minutes += 1
result = minutes if fresh == 0 else -1

# 3) Topological sort (Kahn's): Course Schedule
adj, indeg = defaultdict(list), [0] * n
for course, pre in prerequisites:
    adj[pre].append(course)
    indeg[course] += 1
q = deque(i for i in range(n) if indeg[i] == 0)
order = []
while q:
    node = q.popleft()
    order.append(node)
    for nei in adj[node]:
        indeg[nei] -= 1
        if indeg[nei] == 0:
            q.append(nei)
can_finish = len(order) == n              # otherwise there's a cycle

# 4) Union-Find (path compression + union by size)
parent, size = list(range(n)), [1] * n
def find(x):
    while parent[x] != x:
        parent[x] = parent[parent[x]]
        x = parent[x]
    return x
def union(a, b):
    ra, rb = find(a), find(b)
    if ra == rb:
        return False                        # already connected: this edge is redundant
    if size[ra] < size[rb]:
        ra, rb = rb, ra
    parent[rb] = ra
    size[ra] += size[rb]
    return True
```

## Tricks to remember
- **Reverse thinking:** Pacific Atlantic and Surrounded Regions are easier if you DFS **from the borders inward**.
- **Clone Graph:** hashmap `old → new`, DFS. Create the clone *before* recursing on neighbors.
- **Graph Valid Tree:** exactly `n - 1` edges **and** connected (or: no union returns False).
- **Word Ladder:** BFS over words. Neighbors via patterns like `h*t` → list of words.
- Adjacency list for an undirected graph: add **both** directions.

## Common mistakes
- Marking visited when **popping** instead of when **pushing** (BFS gets duplicates and can TLE).
- Grid bounds checks in the wrong order (check bounds before indexing).
- Deep recursion on big grids: Python's default limit is 1000. Use BFS or `sys.setrecursionlimit`.

## Problems (NeetCode 150)
- [ ] [[Number of Islands]] (Medium)
- [ ] [[Max Area of Island]] (Medium)
- [ ] [[Clone Graph]] (Medium)
- [ ] [[Walls and Gates]] (Medium)
- [ ] [[Rotting Oranges]] (Medium)
- [ ] [[Pacific Atlantic Water Flow]] (Medium)
- [ ] [[Surrounded Regions]] (Medium)
- [ ] [[Course Schedule]] (Medium)
- [ ] [[Course Schedule II]] (Medium)
- [ ] [[Graph Valid Tree]] (Medium)
- [ ] [[Number of Connected Components in an Undirected Graph]] (Medium)
- [ ] [[Redundant Connection]] (Medium)
- [ ] [[Word Ladder]] (Hard)

## My insights
- 

---
Prev: [[Backtracking]] · Next: [[1-D Dynamic Programming]] · [[Home]]
