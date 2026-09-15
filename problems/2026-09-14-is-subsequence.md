# Is Subsequence

**Puzzle date:** 2026-09-14  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the single for loop that iterates over t once, where n is the length of t. You only ever move forward through t, comparing each character to s[i] and incrementing i when there's a match, so the work done is directly proportional to the length of t, giving O(n) time. A tempting but wrong answer is O(m*n), where m is the length of s, since it looks like you're matching two strings against each other; but there's no nested loop or inner scan over s—i only advances forward and the loop breaks early once i reaches len(s), so s's length doesn't multiply into the cost. Space is O(1) because the only extra memory used is the integer index i, regardless of how long s or t are; no arrays, lists, or recursive stacks are created that scale with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def is_subsequence(s: str, t: str) -> bool:
    if not s:
        return True

    i = 0
    for c in t:
        if c == s[i]:
            i += 1
        if i == len(s):
            break
    return i == len(s)
```

### C++

```cpp
bool isSubsequence(std::string s, std::string t) {
    if (s.empty()) {
        return true;
    }

    int i = 0;
    for (char c : t) {
        if (c == s[i]) {
            ++i;
        }
        if (i == (int)s.length()) {
            break;
        }
    }
    return i == (int)s.length();
}
```

### Rust

```rust
fn is_subsequence(s: &str, t: &str) -> bool {
    if s.is_empty() {
        return true;
    }

    let sb = s.as_bytes();
    let mut i = 0usize;
    for &c in t.as_bytes() {
        if c == sb[i] {
            i += 1;
        }
        if i == sb.len() {
            break;
        }
    }
    i == sb.len()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/is-subsequence.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
