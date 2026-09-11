# Implement Trie

**Puzzle date:** 2026-06-28  
**Category:** trie  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

Each operation (insert, search, starts_with) iterates through the characters of the input string one by one, making the dominant cost proportional to the length of the string — O(n) where n is the number of characters. The for-loop in _find and insert drives this cost, visiting exactly one trie node per character. For space, inserting a word of length n creates at most n new Trie nodes in the worst case (when no prefix is shared), so space per insertion is O(n), and total space across all insertions is O(sum of word lengths). You might be tempted to say O(26n) because each node can have up to 26 children (for lowercase letters), but Big-O drops constant factors, so O(26n) simplifies to O(n).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class Trie:
    def __init__(self):
        self.children = {}
        self.end = False

    def insert(self, word: str) -> None:
        node = self
        for ch in word:
            if ch not in node.children:
                node.children[ch] = Trie()
            node = node.children[ch]
        node.end = True

    def search(self, word: str) -> bool:
        node = self._find(word)
        return node is not None and node.end

    def starts_with(self, prefix: str) -> bool:
        return self._find(prefix) is not None

    def _find(self, s: str):
        node = self
        for ch in s:
            if ch not in node.children:
                return None
            node = node.children[ch]
        return node
```

### C++

```cpp
#include <string>
#include <unordered_map>

class Trie {
    std::unordered_map<char, Trie*> children;
    bool end = false;
public:
    void insert(std::string word) {
        Trie* node = this;
        for (char c : word) {
            if (!node->children.count(c)) node->children[c] = new Trie();
            node = node->children[c];
        }
        node->end = true;
    }
    Trie* find(const std::string& s) {
        Trie* node = this;
        for (char c : s) {
            if (!node->children.count(c)) return nullptr;
            node = node->children[c];
        }
        return node;
    }
    bool search(std::string word) { Trie* n = find(word); return n && n->end; }
    bool startsWith(std::string p) { return find(p) != nullptr; }
};
```

### Rust

```rust
use std::collections::HashMap;

struct Trie {
    children: HashMap<char, Trie>,
    end: bool,
}

impl Trie {
    fn new() -> Self { Self { children: HashMap::new(), end: false } }

    fn insert(&mut self, word: &str) {
        let mut node = self;
        for ch in word.chars() {
            node = node.children.entry(ch).or_insert_with(Trie::new);
        }
        node.end = true;
    }

    fn find(&self, s: &str) -> Option<&Trie> {
        let mut node = self;
        for ch in s.chars() {
            node = node.children.get(&ch)?;
        }
        Some(node)
    }

    fn search(&self, word: &str) -> bool { self.find(word).map_or(false, |n| n.end) }
    fn starts_with(&self, prefix: &str) -> bool { self.find(prefix).is_some() }
}
```

---

Played daily at [complexle.com](https://complexle.com).
