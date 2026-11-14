---
tags: [pattern]
phase: 3
order: 18
---
# Bit Manipulation

> [!tip] In one line
> A handful of identities (XOR cancels, `n & (n-1)` drops the lowest bit, shifts read bits) solve most of these in O(1) space.

## Recognize it
- "every element appears twice except one"
- "without using extra space," "without `+` or `-`"
- "count the 1 bits," "power of two," "reverse the bits"
- "missing number in 0..n"

## Identities to memorize
| Expression | Meaning |
|---|---|
| `a ^ a = 0`, `a ^ 0 = a` | XOR cancels pairs |
| `n & 1` | lowest bit (odd?) |
| `n >> 1` | divide by 2 |
| `n & (n - 1)` | remove lowest set bit |
| `n & -n` | isolate lowest set bit |
| `n > 0 and n & (n - 1) == 0` | power of two |
| `(n >> i) & 1` | i-th bit |

## Templates
```python
# 1) Single Number
res = 0
for x in nums:
    res ^= x

# 2) Count set bits
count = 0
while n:
    n &= n - 1
    count += 1

# 3) Counting Bits 0..n with DP
dp = [0] * (n + 1)
for i in range(1, n + 1):
    dp[i] = dp[i >> 1] + (i & 1)

# 4) Reverse 32 bits
res = 0
for i in range(32):
    res = (res << 1) | ((n >> i) & 1)

# 5) Missing Number
res = len(nums)
for i, x in enumerate(nums):
    res ^= i ^ x
```

## Tricks to remember
- **Sum of Two Integers:** `sum = a ^ b` (without carry), `carry = (a & b) << 1`; repeat until carry is 0. In Python, mask with `0xFFFFFFFF` because Python ints are unbounded.
- **Reverse Integer:** pop digits with `%` and `//` (careful with negatives in Python: use `int(x / 10)` or work on `abs`), and check the 32-bit overflow before pushing.

## Common mistakes
- Python's negative numbers and infinite-precision ints: mask to 32 bits when the problem assumes C-style integers.

## Problems (NeetCode 150)
- [ ] [[Single Number]] (Easy)
- [ ] [[Number of 1 Bits]] (Easy)
- [ ] [[Counting Bits]] (Easy)
- [ ] [[Reverse Bits]] (Easy)
- [ ] [[Missing Number]] (Easy)
- [ ] [[Sum of Two Integers]] (Medium)
- [ ] [[Reverse Integer]] (Medium)

## My insights
- 

---
Prev: [[Math & Geometry]] · [[Home]]
