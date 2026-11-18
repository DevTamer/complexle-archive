# Isomorphic Strings

**Puzzle date:** 2026-11-17  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The zip walks both strings together in a single pass, and every operation inside the loop is a constant-time dictionary membership test or insertion, so the running time is linear in the string length. Two maps are needed rather than one because the mapping must be a bijection — checking only one direction would wrongly accept two different characters mapping onto the same target. Space is O(n) because each dictionary holds one entry per distinct character seen, which reaches n when every character in the input is unique.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def is_isomorphic(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False

    s2t: dict[str, str] = {}
    t2s: dict[str, str] = {}
    for p, w in zip(s, t):
        if w not in s2t and p not in t2s:
            s2t[w] = p
            t2s[p] = w
        elif w not in s2t or s2t[w] != p:
            return False
    return True
```

### C++

```cpp
bool isIsomorphic(std::string s, std::string t) {
    if (s.length() != t.length()) {
        return false;
    }
    std::vector<int> s2t(256, 0), t2s(256, 0);
    for (int i = 0; i < (int)s.length(); ++i) {
        if (s2t[(unsigned char)s[i]] == 0 && t2s[(unsigned char)t[i]] == 0) {
            s2t[(unsigned char)s[i]] = t[i];
            t2s[(unsigned char)t[i]] = s[i];
        } else if (s2t[(unsigned char)s[i]] != t[i]) {
            return false;
        }
    }
    return true;
}
```

### Rust

```rust
fn is_isomorphic(s: &str, t: &str) -> bool {
    if s.len() != t.len() {
        return false;
    }
    let s_bytes = s.as_bytes();
    let t_bytes = t.as_bytes();
    let mut s2t: HashMap<u8, u8> = HashMap::new();
    let mut t2s: HashMap<u8, u8> = HashMap::new();
    for i in 0..s_bytes.len() {
        let p = s_bytes[i];
        let w = t_bytes[i];
        if !s2t.contains_key(&w) && !t2s.contains_key(&p) {
            s2t.insert(w, p);
            t2s.insert(p, w);
        } else if !s2t.contains_key(&w) || s2t[&w] != p {
            return false;
        }
    }
    true
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/isomorphic-strings.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
