---
tags: [pattern]
phase: 2
order: 8
---
# Tries

> [!tip] In one line
> A tree of characters where every path from the root spells a prefix, so "does any word start with X?" costs O(len(X)).

## Recognize it
- "prefix," "starts with," "autocomplete"
- Many words searched at once (Word Search II: build a trie of the words, then DFS the grid once)
- Wildcard search like `"b.d"`

## Core idea
Each node = `children: dict[char → node]` + `end: bool` (a word ends here).

## Template
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        cur = self.root
        for c in word:
            cur = cur.children.setdefault(c, TrieNode())
        cur.end = True

    def _walk(self, s):
        cur = self.root
        for c in s:
            if c not in cur.children:
                return None
            cur = cur.children[c]
        return cur

    def search(self, word):
        node = self._walk(word)
        return node is not None and node.end

    def startsWith(self, prefix):
        return self._walk(prefix) is not None
```

```python
# Wildcard "." search: DFS over all children at a dot
def search(self, word):
    def dfs(i, node):
        if i == len(word):
            return node.end
        c = word[i]
        if c == ".":
            return any(dfs(i + 1, child) for child in node.children.values())
        return c in node.children and dfs(i + 1, node.children[c])
    return dfs(0, self.root)
```

## Tricks to remember
- **Word Search II:** insert all words into a trie. DFS from each cell following trie children. When `node.end`, record the word and set `end = False` to avoid duplicates. **Prune** leaf nodes after finding words for speed.
- Storing the whole `word` at the end node (instead of `end = True`) saves rebuilding strings.

## Common mistakes
- `search` returning True for a prefix (you forgot to check `.end`).
- In Word Search II, not marking cells visited during DFS.

## Problems (NeetCode 150)
- [ ] [[Implement Trie Prefix Tree]] (Medium)
- [ ] [[Design Add and Search Words Data Structure]] (Medium)
- [ ] [[Word Search II]] (Hard)

## My insights
- 

---
Prev: [[Trees]] · Next: [[Heap - Priority Queue]] · [[Home]]
