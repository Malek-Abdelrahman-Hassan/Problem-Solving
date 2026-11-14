---
tags: [pattern]
phase: 1
order: 6
---
# Linked List

> [!tip] In one line
> Almost every linked list problem is a combination of four moves: **dummy node, reverse, fast/slow pointers, merge.**

## Recognize it
- Input is a `ListNode`
- "cycle," "middle," "nth from the end" → fast & slow
- "reverse," "reorder," "k-group" → reverse
- "merge sorted" → merge (+ heap for K lists)
- "O(1) get/put with eviction" → hashmap + doubly linked list (LRU)

## Core idea
Draw boxes and arrows on paper. Before changing `node.next`, **save what you'd lose**.

## Templates
```python
# 1) Dummy node: head is never a special case
dummy = ListNode(0, head)
cur = dummy
# ... build or modify ...
return dummy.next

# 2) Reverse
prev, cur = None, head
while cur:
    nxt = cur.next
    cur.next = prev
    prev, cur = cur, nxt
return prev

# 3) Fast & slow
slow = fast = head
while fast and fast.next:
    slow, fast = slow.next, fast.next.next
    if slow is fast:
        return True          # cycle
# after the loop (no cycle): slow is the middle

# 4) Merge two sorted
dummy = cur = ListNode()
while l1 and l2:
    if l1.val <= l2.val:
        cur.next, l1 = l1, l1.next
    else:
        cur.next, l2 = l2, l2.next
    cur = cur.next
cur.next = l1 or l2
return dummy.next
```

## Tricks to remember
- **Nth from end:** move `fast` n steps ahead first, then move both. When `fast` hits the end, `slow` is just before the target.
- **Reorder List:** find middle, reverse second half, merge alternating.
- **Copy List with Random Pointer:** hashmap `old → new` in two passes.
- **Find the Duplicate Number:** treat values as `next` pointers. It becomes cycle detection (Floyd's).
- **LRU Cache:** dict `key → node` + doubly linked list with dummy `left`/`right` sentinels.
- **Merge K Sorted Lists:** min-heap of `(val, i, node)`. The `i` breaks ties so nodes are never compared.

## Common mistakes
- Losing the rest of the list by overwriting `.next` before saving it.
- `while fast.next` without checking `fast` first → `AttributeError` on `None`.
- Returning `head` instead of `dummy.next` when the head can change.

## Problems (NeetCode 150)
- [ ] [[Reverse Linked List]] (Easy)
- [ ] [[Merge Two Sorted Lists]] (Easy)
- [ ] [[Linked List Cycle]] (Easy)
- [ ] [[Reorder List]] (Medium)
- [ ] [[Remove Nth Node From End of List]] (Medium)
- [ ] [[Copy List With Random Pointer]] (Medium)
- [ ] [[Add Two Numbers]] (Medium)
- [ ] [[Find the Duplicate Number]] (Medium)
- [ ] [[LRU Cache]] (Medium)
- [ ] [[Merge K Sorted Lists]] (Hard)
- [ ] [[Reverse Nodes in K-Group]] (Hard)

## My insights
- 

---
Prev: [[Binary Search]] · Next: [[Trees]] · [[Home]]
