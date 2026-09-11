# Reverse String

**Puzzle date:** 2026-09-09  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the while loop, which moves two pointers (i and j) toward each other from opposite ends of the list. Since each iteration swaps one pair of elements and the pointers meet in the middle after about n/2 steps, the loop runs a number of times proportional to n, giving you O(n) time. You might be tempted to think O(n²) because it swaps elements, but there's no nested loop or repeated scanning happening — each element is touched exactly once. For space, the function only uses a constant number of extra variables (i, j, and a temporary swap), and it modifies the list in place rather than creating a new one, so the space complexity stays at O(1) regardless of how large the input list is.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def reverse_string(s: list[str]) -> None:
    i, j = 0, len(s) - 1
    while i < j:
        s[i], s[j] = s[j], s[i]
        i += 1
        j -= 1
```

### C++

```cpp
#include <vector>

void reverseString(std::vector<char>& s) {
    for (int i = 0, j = (int)s.size() - 1; i < j; ++i, --j) {
        std::swap(s[i], s[j]);
    }
}
```

### Rust

```rust
fn reverse_string(s: &mut Vec<char>) {
    if s.is_empty() {
        return;
    }
    let mut i = 0;
    let mut j = s.len() - 1;
    while i < j {
        s.swap(i, j);
        i += 1;
        j -= 1;
    }
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/reverse-string.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
