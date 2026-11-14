---
tags: [pattern]
phase: 3
order: 16
---
# Advanced Graphs

> [!tip] In one line
> [[Graphs]] with **weights**. Use a heap to always expand the cheapest option next (Dijkstra, Prim), or relax edges K times (Bellman-Ford).

## Recognize it
- "shortest / cheapest path" with **weighted** edges (non-negative) → **Dijkstra**
- "connect all points with minimum total cost" → **Minimum Spanning Tree** (Prim / Kruskal)
- "at most K stops" → **Bellman-Ford** (K + 1 rounds)
- "minimize the **maximum** value along a path" (Swim in Rising Water) → Dijkstra with `max` instead of `+`
- "use every edge exactly once" (Reconstruct Itinerary) → **Eulerian path** (Hierholzer)
- "derive an order from sorted words" (Alien Dictionary) → **topological sort** on letters

## Templates
```python
import heapq
from collections import defaultdict

# 1) Dijkstra
def dijkstra(n, edges, src):
    adj = defaultdict(list)
    for u, v, w in edges:
        adj[u].append((v, w))
    dist = {}
    heap = [(0, src)]
    while heap:
        d, node = heapq.heappop(heap)
        if node in dist:
            continue                        # already finalized with a smaller d
        dist[node] = d
        for nei, w in adj[node]:
            if nei not in dist:
                heapq.heappush(heap, (d + w, nei))
    return dist                             # Network Delay = max(dist) if len == n

# 2) Prim's MST (dense graph of points)
def minCostConnectPoints(points):
    n = len(points)
    seen, total = set(), 0
    heap = [(0, 0)]                         # (cost, point index)
    while len(seen) < n:
        cost, i = heapq.heappop(heap)
        if i in seen:
            continue
        seen.add(i)
        total += cost
        for j in range(n):
            if j not in seen:
                d = abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1])
                heapq.heappush(heap, (d, j))
    return total

# 3) Bellman-Ford with at most k stops
def cheapest(n, flights, src, dst, k):
    prices = [float("inf")] * n
    prices[src] = 0
    for _ in range(k + 1):
        tmp = prices[:]                     # copy: use only last round's values
        for u, v, w in flights:
            if prices[u] + w < tmp[v]:
                tmp[v] = prices[u] + w
        prices = tmp
    return prices[dst] if prices[dst] != float("inf") else -1
```

## Tricks to remember
- **Dijkstra doesn't work with negative weights.** Use Bellman-Ford there.
- **Reconstruct Itinerary:** sort destinations, DFS, and append the airport to the route **after** exploring all its edges (post-order). Reverse at the end.
- **Alien Dictionary:** compare adjacent words; the first differing char gives an edge. Invalid if a word is a prefix of the previous, longer word.
- **Swim in Rising Water:** heap of `(max_height_so_far, r, c)`.

## Common mistakes
- Not skipping already-finalized nodes when popping (slow, sometimes wrong).
- Bellman-Ford without copying the array: a single round may chain more than one edge and break the K-stops limit.

## Problems (NeetCode 150)
- [ ] [[Network Delay Time]] (Medium)
- [ ] [[Reconstruct Itinerary]] (Hard)
- [ ] [[Min Cost to Connect All Points]] (Medium)
- [ ] [[Swim in Rising Water]] (Hard)
- [ ] [[Alien Dictionary]] (Hard)
- [ ] [[Cheapest Flights Within K Stops]] (Medium)

## My insights
- 

---
Prev: [[Intervals]] · Next: [[Math & Geometry]] · [[Home]]
