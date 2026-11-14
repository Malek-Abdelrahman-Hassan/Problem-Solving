---
tags: [pattern, cheatsheet]
---
# Pattern Recognition Cheatsheet

> [!tip] How to use
> Read the problem, then scan this page. Underline every trigger word in the problem statement. Two or three matches usually point to one pattern.

## Constraints tell you the complexity
LeetCode allows roughly **10⁸ simple operations**. Work backwards from `n`:

| n up to | Target complexity | Usually means |
|---|---|---|
| ≤ 10 | O(n!) | permutations, [[Backtracking]] |
| ≤ 20 | O(2ⁿ) | subsets, [[Backtracking]], bitmask |
| ≤ 500 | O(n³) | 3 nested loops, interval DP |
| ≤ 5,000 | O(n²) | [[2-D Dynamic Programming]], nested loops |
| ≤ 10⁵ – 10⁶ | O(n log n) or O(n) | sort, [[Heap - Priority Queue]], [[Sliding Window]], [[Two Pointers]], hashing |
| ≥ 10⁹ (values) | O(log n) | [[Binary Search]] (often "on the answer"), math |

## "I see X, so I try Y"

### Arrays / strings
| Trigger in the problem | Try |
|---|---|
| "contains duplicate," "count frequency," "anagram," "have we seen it" | [[Arrays & Hashing]] (set / counter) |
| "find pair that sums to target," unsorted | [[Arrays & Hashing]] (hashmap of complements) |
| **sorted** array + pair / triplet | [[Two Pointers]] (from both ends) |
| "palindrome," "reverse in place" | [[Two Pointers]] |
| "in-place," "remove duplicates," "move zeros" | [[Two Pointers]] (read/write pointers) |
| "**contiguous** subarray / substring" + longest / shortest / at most K | [[Sliding Window]] |
| "subarray sum equals K" with negatives | prefix sum + hashmap ([[Arrays & Hashing]]) |
| "maximum subarray sum" | [[Greedy]] (Kadane) |
| "window of size k," "max in every window" | [[Sliding Window]] (+ monotonic deque) |
| "next greater / smaller element," "days until warmer" | [[Stack]] (monotonic) |
| "matching brackets," "nested," "undo," "evaluate expression" | [[Stack]] |
| "sorted" + "find" / "search," or "minimum X such that…" | [[Binary Search]] |
| "rotated sorted array" | [[Binary Search]] (find the sorted half) |
| "top K," "K largest / smallest / closest," "K most frequent" | [[Heap - Priority Queue]] (or bucket sort) |
| "median of a stream" | [[Heap - Priority Queue]] (two heaps) |
| "intervals," "meetings," "overlapping ranges" | [[Intervals]] (sort by start) |
| "prefix," "starts with," "dictionary of words," "autocomplete" | [[Tries]] |

### Linked lists
| Trigger | Try |
|---|---|
| "cycle," "middle of list," "nth from end" | [[Linked List]] (fast & slow pointers) |
| "reverse," "reorder," "k-group" | [[Linked List]] (reverse template + dummy node) |
| "merge sorted lists" | [[Linked List]] (merge) + [[Heap - Priority Queue]] for K lists |
| "O(1) get and put," "LRU" | hashmap + doubly linked list |

### Trees / graphs
| Trigger | Try |
|---|---|
| binary tree, "depth," "path," "balanced," "same tree" | [[Trees]] (DFS: what does each node return?) |
| "level by level," "right side view," "minimum depth" | [[Trees]] (BFS with a queue) |
| BST + "kth smallest," "validate" | [[Trees]] (in-order is sorted) |
| grid of `'1'/'0'`, "islands," "regions," "flood fill" | [[Graphs]] (DFS/BFS on grid) |
| "shortest path," **unweighted**, "minimum steps" | [[Graphs]] (BFS) |
| "spreads from many sources at once" (rotting, gates) | [[Graphs]] (multi-source BFS) |
| "prerequisites," "order of tasks," "dependencies" | [[Graphs]] (topological sort) |
| "connected components," "redundant edge," "is it a tree" | [[Graphs]] (Union-Find or DFS) |
| "shortest path," **weighted, non-negative** | [[Advanced Graphs]] (Dijkstra) |
| "connect all points with minimum cost" | [[Advanced Graphs]] (Prim / Kruskal MST) |
| "at most K stops / edges" | [[Advanced Graphs]] (Bellman-Ford) |

### Choices / optimization
| Trigger | Try |
|---|---|
| "all combinations / permutations / subsets," "generate all" | [[Backtracking]] |
| "place N items with constraints" (N-Queens, sudoku) | [[Backtracking]] |
| "**number of ways**," "min / max cost," "can you reach," choices at each step | [[1-D Dynamic Programming]] |
| two strings / grid + "number of ways," "min edits," "longest common" | [[2-D Dynamic Programming]] |
| "can you reach the end," "minimum jumps," a locally best choice seems to work | [[Greedy]] |
| "single number," "without extra space," "XOR," "bits," "power of two" | [[Bit Manipulation]] |
| "rotate matrix," "spiral," "in-place matrix" | [[Math & Geometry]] |

## Backtracking vs. DP vs. Greedy
- Want **every** solution (list them all)? **Backtracking**
- Want a **count** or **best value**, and subproblems repeat? **DP**
- Can you prove that taking the locally best choice never hurts? **Greedy** (if unsure, DP is safer)

## Big-O quick reference (Python)
| Operation | Cost |
|---|---|
| `x in set` / `dict[k]` | O(1) avg |
| `x in list` | O(n) |
| `list.append` / `list.pop()` | O(1) |
| `list.pop(0)` / `list.insert(0, x)` | O(n), so use `collections.deque` |
| `heapq.heappush` / `heappop` | O(log n) |
| `sorted(arr)` | O(n log n) |
| `s[a:b]` slicing | O(b − a) |
| string `+=` in a loop | O(n²) total, so collect into a list and `"".join()` |
