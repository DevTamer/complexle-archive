# Word Pattern

**Puzzle date:** 2026-11-22  
**Category:** hash map  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(n + m)`

## Explanation

word_count scans the sentence once, and the main loop consumes the word generator alongside the pattern, so each character of the sentence and each character of the pattern is handled a constant number of times, giving O(n + m). The generator matters: it yields one word at a time instead of materialising a list of every word first. Space is still O(n + m) because the two dictionaries hold one entry per distinct word and per distinct pattern character, and in the worst case — every word distinct — that scales with the sentence.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def word_pattern(pattern: str, s: str) -> bool:
    def word_count(s: str) -> int:
        cnt = 1 if s else 0
        for c in s:
            if c == ' ':
                cnt += 1
        return cnt

    def word_generator(s: str):
        w = ""
        for c in s:
            if c == ' ':
                yield w
                w = ""
            else:
                w += c
        yield w

    if len(pattern) != word_count(s):
        return False

    w2p: dict[str, str] = {}
    p2w: dict[str, str] = {}
    for p, w in zip(pattern, word_generator(s)):
        if w not in w2p and p not in p2w:
            w2p[w] = p
            p2w[p] = w
        elif w not in w2p or w2p[w] != p:
            return False
    return True
```

### C++

```cpp
bool wordPattern(std::string pattern, std::string str) {
    int cnt = str.empty() ? 0 : 1;
    for (const auto& c : str) {
        if (c == ' ') {
            ++cnt;
        }
    }
    if ((int)pattern.size() != cnt) {
        return false;
    }

    std::unordered_map<std::string, char> w2p;
    std::unordered_map<char, std::string> p2w;
    size_t i = 0, j = 0;
    for (const auto& p : pattern) {
        j = str.find(' ', i);
        if (j == std::string::npos) {
            j = str.length();
        }
        const std::string w = str.substr(i, j - i);

        if (!w2p.count(w) && !p2w.count(p)) {
            w2p[w] = p;
            p2w[p] = w;
        } else if (!w2p.count(w) || w2p[w] != p) {
            return false;
        }
        i = j + 1;
    }
    return true;
}
```

### Rust

```rust
fn word_pattern(pattern: &str, s: &str) -> bool {
    fn word_count(s: &str) -> usize {
        let mut cnt = if s.is_empty() { 0 } else { 1 };
        for c in s.chars() {
            if c == ' ' {
                cnt += 1;
            }
        }
        cnt
    }

    if pattern.chars().count() != word_count(s) {
        return false;
    }

    let mut w2p: HashMap<&str, char> = HashMap::new();
    let mut p2w: HashMap<char, &str> = HashMap::new();

    let mut start = 0usize;
    for p in pattern.chars() {
        let end = match s[start..].find(' ') {
            Some(pos) => start + pos,
            None => s.len(),
        };
        let w = &s[start..end];
        start = end + 1;

        if !w2p.contains_key(w) && !p2w.contains_key(&p) {
            w2p.insert(w, p);
            p2w.insert(p, w);
        } else if !w2p.contains_key(w) || w2p[w] != p {
            return false;
        }
    }
    true
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/word-pattern.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
