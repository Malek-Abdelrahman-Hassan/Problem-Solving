---
tags: [pattern]
phase: 1
order: 2
---
# Two Pointers

> [!tip] In one line
> Two indices moving through the data so you can **rule out many options per step** and turn O(n²) into O(n).

## Recognize it
- Array is **sorted** (or you can sort it) and you need a pair / triplet
- "palindrome," "reverse," compare from both ends
- "in-place," "remove duplicates," "move zeros" (read/write pointers)
- "container," "trap water": the answer depends on the left and right boundaries

## Core idea
With pointers at both ends of a sorted array, each comparison tells you **which pointer can't be part of a better answer**, so you move that one.

## Templates
```python
# 1) Opposite ends (sorted array, pair sum)
l, r = 0, len(nums) - 1
while l < r:
    s = nums[l] + nums[r]
    if s == target:
        return [l, r]
    if s < target:
        l += 1      # need bigger
    else:
        r -= 1      # need smaller

# 2) 3Sum: fix one, two-pointer the rest
nums.sort()
res = []
for i in range(len(nums)):
    if i > 0 and nums[i] == nums[i - 1]:
        continue
    l, r = i + 1, len(nums) - 1
    while l < r:
        s = nums[i] + nums[l] + nums[r]
        if s < 0:
            l += 1
        elif s > 0:
            r -= 1
        else:
            res.append([nums[i], nums[l], nums[r]])
            l += 1
            while l < r and nums[l] == nums[l - 1]:
                l += 1

# 3) Read / write pointers (in-place)
w = 0
for r in range(len(nums)):
    if keep(nums[r]):
        nums[w] = nums[r]
        w += 1
```

## Tricks to remember
- **Container With Most Water:** always move the **shorter** side. The taller one can't do better with a narrower width.
- **Trapping Rain Water:** water at i = `min(maxLeft, maxRight) - height[i]`. With two pointers, move the side with the smaller max.
- **Valid Palindrome:** skip non-alphanumeric with inner `while` loops, compare `.lower()`.

## Common mistakes
- Forgetting to **sort** first.
- Not skipping duplicates in 3Sum, which produces repeated triplets.
- `l <= r` vs `l < r`: for pairs you need two distinct elements, so use `<`.

## Problems (NeetCode 150)
- [ ] [[Valid Palindrome]] (Easy)
- [ ] [[Two Sum II Input Array Is Sorted]] (Medium)
- [ ] [[3Sum]] (Medium)
- [ ] [[Container With Most Water]] (Medium)
- [ ] [[Trapping Rain Water]] (Hard)

## My insights
- 

---
Prev: [[Arrays & Hashing]] · Next: [[Sliding Window]] · [[Home]]
