# Valid Anagram

**Puzzle date:** 2026-07-19  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the two sequential for-loops, one over string s and one over string t, each running in O(n) where n is the length of the strings. Since these loops run one after the other (not nested), the total time is O(n) + O(n) = O(n). You might be tempted to say O(26n) because of the fixed-size counts array, but the constant factor of 26 is dropped in Big-O notation, keeping it O(n). The space complexity is O(1) because the counts array is always exactly 26 integers regardless of the input size — it does not grow with n, making it constant space even though you allocate an array.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def is_anagram(s: str, t: str) -> bool:
    # s and t consist of lowercase English letters only.
    if len(s) != len(t):
        return False
    counts = [0] * 26
    for c in s:
        counts[ord(c) - ord('a')] += 1
    for c in t:
        i = ord(c) - ord('a')
        counts[i] -= 1
        if counts[i] < 0:
            return False
    return True
```

### C++

```cpp
#include <string>
#include <array>

// s and t consist of lowercase English letters only.
bool isAnagram(std::string s, std::string t) {
    if (s.size() != t.size()) return false;
    std::array<int, 26> counts{};
    for (char c : s) counts[c - 'a']++;
    for (char c : t) {
        if (--counts[c - 'a'] < 0) return false;
    }
    return true;
}
```

### Rust

```rust
// s and t consist of lowercase English letters only.
fn is_anagram(s: &str, t: &str) -> bool {
    if s.len() != t.len() {
        return false;
    }
    let mut counts = [0i32; 26];
    for c in s.bytes() {
        counts[(c - b'a') as usize] += 1;
    }
    for c in t.bytes() {
        let i = (c - b'a') as usize;
        counts[i] -= 1;
        if counts[i] < 0 {
            return false;
        }
    }
    true
}
```

---

Played daily at [complexle.com](https://complexle.com).
