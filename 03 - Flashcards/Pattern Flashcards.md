---
tags: [flashcards]
---
#flashcards/patterns

# Pattern Flashcards

> [!tip] How to use
> **Without a plugin:** cover the right side of `::` and answer out loud.
> **With the Spaced Repetition plugin:** click "Review flashcards" and the plugin schedules the cards for you.
> **Add a card** whenever you meet a trigger you missed. Format: `question::answer` on one line.

## Triggers → pattern
Contiguous subarray/substring + longest/shortest/at most K::Sliding Window (variable size, shrink while invalid)
Sorted array + find a pair with a given sum::Two Pointers from both ends
Unsorted array + find a pair with a given sum::Hashmap of value → index (check complement before inserting)
Next greater / next warmer / next smaller element::Monotonic stack of indices
Matching brackets or nested structure::Stack
Sorted input or "minimum X such that condition holds"::Binary Search (on the array, or on the answer)
Top K / K largest / K closest::Heap of size K (min-heap for K largest)
Median of a data stream::Two heaps: max-heap for the low half, min-heap for the high half
Cycle in linked list / middle of list::Fast & slow pointers
Tree depth / path / balanced / diameter::DFS where each call returns a value to its parent
Level-by-level tree / shortest path in unweighted graph::BFS with a queue
Grid of land and water, count islands::DFS/BFS from each unvisited land cell, mark visited
Prerequisites / task ordering / dependencies::Topological sort (Kahn's BFS with indegrees)
Connected components / redundant edge::Union-Find
Shortest path with non-negative weights::Dijkstra (min-heap of (dist, node))
Generate all subsets / permutations / combinations::Backtracking (choose, explore, un-choose)
Number of ways / min cost / can reach, with repeated subproblems::Dynamic Programming
Two strings compared (LCS, edit distance)::2-D DP with dp[i][j] over prefixes
Merge / insert / overlapping intervals::Sort by start, compare with the last merged end
Minimum number of meeting rooms::Sort starts, min-heap of end times (or sweep line)
Remove minimum intervals to make non-overlapping::Sort by END, greedily keep the earliest-ending
Every number appears twice except one::XOR everything
Words sharing prefixes / search many words in a grid::Trie
Maximum subarray sum::Kadane: reset running sum when it goes negative
n ≤ 20::Exponential is fine: backtracking or bitmask
n ≤ 10^5::Need O(n log n) or O(n)

## Pattern → core idea
Sliding window loop shape::for right in range(n): add s[right]; while invalid: remove s[left], left += 1; update answer
Binary search on answer shape::lo, hi = min possible, max possible; while lo < hi: mid; if feasible(mid): hi = mid else lo = mid + 1
Reverse a linked list (3 lines in the loop)::nxt = cur.next; cur.next = prev; prev, cur = cur, nxt
Why use a dummy node in linked lists?::So the head is not a special case; return dummy.next
Backtracking shape::append choice → recurse → pop choice
Skip duplicates in backtracking::Sort first; in the loop, skip if i > start and nums[i] == nums[i-1]
Four DP steps::1) state: what dp[i] means  2) recurrence  3) base cases  4) order / answer location
House Robber recurrence::dp[i] = max(dp[i-1], dp[i-2] + nums[i])
Coin Change recurrence::dp[a] = min(dp[a], dp[a - coin] + 1) for each coin
LCS recurrence::if a[i]==b[j]: 1 + dp[i+1][j+1] else max(dp[i+1][j], dp[i][j+1])
Max-heap in Python::heapq with negated values: push -x, pop and negate back
Topological sort detects a cycle when::fewer nodes are processed than exist (some indegree never hits 0)
Validate BST::DFS passing (low, high) bounds down, not just comparing with children
Rotate matrix 90° clockwise::Transpose, then reverse each row
n & (n - 1)::Removes the lowest set bit (count bits, power of two check)
