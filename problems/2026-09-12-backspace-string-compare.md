# Backspace String Compare

**Puzzle date:** 2026-09-12  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the two pointers i and j scanning through s and t from the back, where each character is visited a constant number of times across the calls to find_next_char and the outer while loop. Even though find_next_char is called repeatedly inside a loop, the inner index it moves only ever decreases, so the total work across all calls is bounded by the combined lengths of s and t, giving you linear time O(n). You might be tempted to think it's O(n^2) because there's a loop inside a loop (the while loop calling a function with its own while loop), but the inner loop doesn't restart from scratch each time—it continues from where the pointer left off, so no character is reprocessed. Space-wise, the algorithm only uses a handful of integer variables (i, j, skip) and doesn't build any new strings or data structures, so it runs in constant O(1) space regardless of input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def backspace_compare(s: str, t: str) -> bool:
    def find_next_char(chars: str, i: int) -> tuple[str, int]:
        skip = 0
        while i >= 0:
            if chars[i] == '#':
                skip += 1
                i -= 1
            elif skip > 0:
                skip -= 1
                i -= 1
            else:
                return chars[i], i
        return '\0', i

    i, j = len(s) - 1, len(t) - 1
    while i >= 0 or j >= 0:
        ci, i = find_next_char(s, i)
        cj, j = find_next_char(t, j)
        if ci != cj:
            return False
        i -= 1
        j -= 1
    return True
```

### C++

```cpp
using namespace std;

char findNextChar(const string& s, int& i) {
    int skip = 0;
    for (; i >= 0; --i) {
        if (s[i] == '#') {
            ++skip;
        } else if (skip > 0) {
            --skip;
        } else {
            return s[i];
        }
    }
    return '\0';
}

bool backspaceCompare(string S, string T) {
    for (int i = S.length() - 1, j = T.length() - 1; i >= 0 || j >= 0; --i, --j) {
        if (findNextChar(S, i) != findNextChar(T, j)) {
            return false;
        }
    }
    return true;
}
```

### Rust

```rust
fn find_next_char(bytes: &[u8], i: &mut isize) -> Option<u8> {
    let mut skip = 0;
    while *i >= 0 {
        let idx = *i as usize;
        if bytes[idx] == b'#' {
            skip += 1;
            *i -= 1;
        } else if skip > 0 {
            skip -= 1;
            *i -= 1;
        } else {
            return Some(bytes[idx]);
        }
    }
    None
}

fn backspace_compare(s: &str, t: &str) -> bool {
    let s_bytes = s.as_bytes();
    let t_bytes = t.as_bytes();
    let mut i = s_bytes.len() as isize - 1;
    let mut j = t_bytes.len() as isize - 1;
    while i >= 0 || j >= 0 {
        let ci = find_next_char(s_bytes, &mut i);
        let cj = find_next_char(t_bytes, &mut j);
        if ci != cj {
            return false;
        }
        i -= 1;
        j -= 1;
    }
    true
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/backspace-string-compare.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
