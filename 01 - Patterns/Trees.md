---
tags: [pattern]
phase: 2
order: 7
---
# Trees

> [!tip] In one line
> Trust the recursion: decide **what each node returns to its parent**, handle `None`, and combine the left and right results.

## Recognize it
- Input is a `TreeNode`
- "depth," "height," "diameter," "balanced," "path sum," "same / subtree" → **DFS**
- "level order," "right side view," "each level" → **BFS**
- **BST** → in-order traversal is sorted; go left or right by comparing values

## Core idea
Before coding, answer three questions:
1. **Base case:** what do I return for `None`?
2. **Return value:** what does a node return to its parent? (height? bool? max path?)
3. **Global answer:** is the answer the return value, or something I track **on the side** (like diameter)?

## Templates
```python
# 1) DFS returning a value (height)
def height(node):
    if not node:
        return 0
    return 1 + max(height(node.left), height(node.right))

# 2) DFS + global answer (diameter / max path sum)
def diameter(root):
    best = 0
    def dfs(node):
        nonlocal best
        if not node:
            return 0
        l, r = dfs(node.left), dfs(node.right)
        best = max(best, l + r)        # path THROUGH this node
        return 1 + max(l, r)           # path going UP to parent (one side only)
    dfs(root)
    return best

# 3) BFS level order
from collections import deque
res, q = [], deque([root] if root else [])
while q:
    level = []
    for _ in range(len(q)):            # exactly one level
        node = q.popleft()
        level.append(node.val)
        if node.left:  q.append(node.left)
        if node.right: q.append(node.right)
    res.append(level)

# 4) Pass info DOWN (validate BST with bounds)
def valid(node, lo=float("-inf"), hi=float("inf")):
    if not node:
        return True
    if not (lo < node.val < hi):
        return False
    return valid(node.left, lo, node.val) and valid(node.right, node.val, hi)
```

## Tricks to remember
- **Info goes up** (return values) vs. **info goes down** (parameters). Count Good Nodes and Validate BST pass info *down*.
- **Max Path Sum:** return `node.val + max(0, left, right)` upward. Update the global answer with `node.val + max(0,l) + max(0,r)`.
- **LCA of BST:** both smaller → go left, both bigger → go right, else current node.
- **Kth Smallest in BST:** iterative in-order with a stack, stop at k.
- **Build from Preorder + Inorder:** `preorder[0]` is the root. Its index in inorder splits left/right. Use a hashmap for the index.
- **Serialize:** preorder with `"N"` for None. Deserialize with an iterator.

## Common mistakes
- Forgetting the `None` base case.
- Validate BST by only comparing with children (wrong; you need bounds).
- Returning the "through" path to the parent (a path can't fork).

## Problems (NeetCode 150)
- [ ] [[Invert Binary Tree]] (Easy)
- [ ] [[Maximum Depth of Binary Tree]] (Easy)
- [ ] [[Diameter of Binary Tree]] (Easy)
- [ ] [[Balanced Binary Tree]] (Easy)
- [ ] [[Same Tree]] (Easy)
- [ ] [[Subtree of Another Tree]] (Easy)
- [ ] [[Lowest Common Ancestor of a Binary Search Tree]] (Medium)
- [ ] [[Binary Tree Level Order Traversal]] (Medium)
- [ ] [[Binary Tree Right Side View]] (Medium)
- [ ] [[Count Good Nodes in Binary Tree]] (Medium)
- [ ] [[Validate Binary Search Tree]] (Medium)
- [ ] [[Kth Smallest Element in a BST]] (Medium)
- [ ] [[Construct Binary Tree From Preorder and Inorder Traversal]] (Medium)
- [ ] [[Binary Tree Maximum Path Sum]] (Hard)
- [ ] [[Serialize and Deserialize Binary Tree]] (Hard)

## My insights
- 

---
Prev: [[Linked List]] · Next: [[Tries]] · [[Home]]
