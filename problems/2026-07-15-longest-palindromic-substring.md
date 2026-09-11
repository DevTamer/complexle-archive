# Longest Palindromic Substring

**Puzzle date:** 2026-07-15  
**Category:** two pointers  
**Time complexity:** `O(n²)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the outer for-loop iterating over each of the n characters, and for each character calling expand() which can itself expand outward up to O(n) steps in the worst case (e.g., a string of all identical characters). This gives you O(n) * O(n) = O(n²) total work. The most tempting wrong answer is O(n) — you might think expand() is cheap on average, but in the worst case every expansion touches the full string. For space, the algorithm only uses a fixed number of variables (start, end, l, r) regardless of input size, so it is O(1) extra space; the O(n) distractor is tempting because of the output string slice, but that is typically not counted as auxiliary space.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def longest_palindrome(s: str) -> str:
    if not s:
        return ""
    start, end = 0, 0
    def expand(l, r):
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return l + 1, r - 1
    for i in range(len(s)):
        l1, r1 = expand(i, i)
        if r1 - l1 > end - start:
            start, end = l1, r1
        l2, r2 = expand(i, i + 1)
        if r2 - l2 > end - start:
            start, end = l2, r2
    return s[start:end + 1]
```

### C++

```cpp
#include <string>
#include <utility>

std::pair<int, int> expand(const std::string& s, int l, int r) {
    while (l >= 0 && r < (int)s.size() && s[l] == s[r]) {
        l--; r++;
    }
    return {l + 1, r - 1};
}

std::string longestPalindrome(std::string s) {
    if (s.empty()) return "";
    int start = 0, end = 0;
    for (int i = 0; i < (int)s.size(); i++) {
        auto [l1, r1] = expand(s, i, i);
        if (r1 - l1 > end - start) { start = l1; end = r1; }
        auto [l2, r2] = expand(s, i, i + 1);
        if (r2 - l2 > end - start) { start = l2; end = r2; }
    }
    return s.substr(start, end - start + 1);
}
```

### Rust

```rust
fn expand(s: &[u8], mut l: i32, mut r: i32) -> (i32, i32) {
    while l >= 0 && (r as usize) < s.len() && s[l as usize] == s[r as usize] {
        l -= 1;
        r += 1;
    }
    (l + 1, r - 1)
}

fn longest_palindrome(s: &str) -> &str {
    let bytes = s.as_bytes();
    if bytes.is_empty() {
        return "";
    }
    let (mut start, mut end) = (0i32, 0i32);
    for i in 0..bytes.len() as i32 {
        let (l1, r1) = expand(bytes, i, i);
        if r1 - l1 > end - start {
            start = l1;
            end = r1;
        }
        let (l2, r2) = expand(bytes, i, i + 1);
        if r2 - l2 > end - start {
            start = l2;
            end = r2;
        }
    }
    &s[start as usize..=end as usize]
}
```

---

Played daily at [complexle.com](https://complexle.com).
