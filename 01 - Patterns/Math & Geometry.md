---
tags: [pattern]
phase: 3
order: 17
---
# Math & Geometry

> [!tip] In one line
> Mostly **matrix index manipulation** plus a few classic math tricks. The challenge is careful bookkeeping, not a clever pattern.

## Recognize it
- "rotate the matrix," "spiral order," "set zeroes," "in place"
- Digit manipulation: "plus one," "happy number," "multiply strings"
- "compute `x^n`" → fast exponentiation

## Templates
```python
# 1) Rotate 90° clockwise, in place: transpose + reverse rows
n = len(matrix)
for i in range(n):
    for j in range(i + 1, n):
        matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
for row in matrix:
    row.reverse()

# 2) Spiral order: shrink four boundaries
res = []
top, bottom, left, right = 0, len(m) - 1, 0, len(m[0]) - 1
while top <= bottom and left <= right:
    for c in range(left, right + 1):   res.append(m[top][c])
    top += 1
    for r in range(top, bottom + 1):   res.append(m[r][right])
    right -= 1
    if top <= bottom:
        for c in range(right, left - 1, -1): res.append(m[bottom][c])
        bottom -= 1
    if left <= right:
        for r in range(bottom, top - 1, -1): res.append(m[r][left])
        left += 1

# 3) Fast power: O(log n)
def myPow(x, n):
    if n < 0:
        x, n = 1 / x, -n
    result = 1
    while n:
        if n & 1:
            result *= x
        x *= x
        n >>= 1
    return result

# 4) Digit loop
while n:
    digit = n % 10
    n //= 10
```

## Tricks to remember
- **Set Matrix Zeroes (O(1) space):** use the first row/col as markers, plus one flag for the first row.
- **Happy Number:** cycle detection. Use a `seen` set, or fast/slow like [[Linked List]].
- **Multiply Strings:** `result[i + j + 1] += d1 * d2`, then carry from the right.
- **Detect Squares:** count points. For a query point, loop over points that could be its **diagonal** corner and multiply the counts of the other two corners.

## Common mistakes
- Spiral: forgetting the `if top <= bottom` / `if left <= right` checks (duplicates on non-square matrices).
- Pow: negative exponents.

## Problems (NeetCode 150)
- [ ] [[Rotate Image]] (Medium)
- [ ] [[Spiral Matrix]] (Medium)
- [ ] [[Set Matrix Zeroes]] (Medium)
- [ ] [[Happy Number]] (Easy)
- [ ] [[Plus One]] (Easy)
- [ ] [[Pow(x, n)]] (Medium)
- [ ] [[Multiply Strings]] (Medium)
- [ ] [[Detect Squares]] (Medium)

## My insights
- 

---
Prev: [[Advanced Graphs]] · Next: [[Bit Manipulation]] · [[Home]]
