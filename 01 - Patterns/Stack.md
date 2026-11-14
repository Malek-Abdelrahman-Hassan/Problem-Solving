---
tags: [pattern]
phase: 1
order: 4
---
# Stack

> [!tip] In one line
> Last in, first out. Use it when the **most recent unresolved thing** is the one you need next: open brackets, pending numbers, elements waiting for their "next greater."

## Recognize it
- Matching / nesting: brackets, tags, "valid"
- "Evaluate expression," "reverse Polish notation"
- "**Next greater / smaller** element," "how many days until warmer"
- "Largest rectangle," "car fleet": elements waiting to be resolved by a later element

## Core idea
- **Plain stack:** push when something opens, pop when it closes.
- **Monotonic stack:** keep the stack sorted (increasing or decreasing). When a new element breaks the order, it's the **answer** for everything you pop.

## Templates
```python
# 1) Matching brackets
pairs = {")": "(", "]": "[", "}": "{"}
stack = []
for c in s:
    if c in pairs:
        if not stack or stack[-1] != pairs[c]:
            return False
        stack.pop()
    else:
        stack.append(c)
return not stack

# 2) Monotonic decreasing stack: next GREATER element (store indices)
res = [0] * len(temps)
stack = []                                  # indices, temps decreasing
for i, t in enumerate(temps):
    while stack and temps[stack[-1]] < t:
        j = stack.pop()
        res[j] = i - j                      # i is j's "next warmer day"
    stack.append(i)

# 3) Min Stack: store (value, min_so_far) pairs
stack.append((val, min(val, stack[-1][1] if stack else val)))
```

## Tricks to remember
- Store **indices**, not values, when you need distances or widths.
- **Largest Rectangle in Histogram:** increasing stack. When popping a bar, its rectangle extends back to where it started, so push the popped start index with the new height.
- **Car Fleet:** sort by position descending, compute time to target. A car that arrives no later than the fleet ahead joins it (don't push).
- **Generate Parentheses** is really [[Backtracking]]: add "(" if open < n, add ")" if close < open.

## Common mistakes
- Popping from an empty stack. Always check `if stack` first.
- Forgetting the final check: the stack must be empty at the end for valid brackets.
- In RPN, the operand order for `-` and `/`: `b = pop(); a = pop(); a - b`. Also use `int(a / b)` to truncate toward zero.

## Problems (NeetCode 150)
- [ ] [[Valid Parentheses]] (Easy)
- [ ] [[Min Stack]] (Medium)
- [ ] [[Evaluate Reverse Polish Notation]] (Medium)
- [ ] [[Generate Parentheses]] (Medium)
- [ ] [[Daily Temperatures]] (Medium)
- [ ] [[Car Fleet]] (Medium)
- [ ] [[Largest Rectangle in Histogram]] (Hard)

## My insights
- 

---
Prev: [[Sliding Window]] · Next: [[Binary Search]] · [[Home]]
