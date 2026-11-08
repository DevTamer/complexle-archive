# Remove Duplicate Letters

**Puzzle date:** 2026-11-07  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

Building the Counter is one linear pass. The main loop looks quadratic because of the inner while, but it is a monotonic stack guarded by in_stack: a character is pushed at most once and popped at most once for the entire run, so the inner loop performs at most n operations in total rather than per iteration. That amortises to O(n). Space is O(n) in the general case — the counter, the stack, and the membership set each hold at most one entry per distinct character, which is bounded by the length of the input when every character is unique.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def remove_duplicate_letters(s: str) -> str:
    remaining = Counter(s)
    in_stack: set[str] = set()
    stk: list[str] = []
    for c in s:
        if c not in in_stack:
            while stk and stk[-1] > c and remaining[stk[-1]]:
                in_stack.remove(stk.pop())
            stk.append(c)
            in_stack.add(c)
        remaining[c] -= 1
    return "".join(stk)
```

### C++

```cpp
std::string removeDuplicateLetters(std::string s) {
    const int k = 26;
    std::vector<int> remaining(k, 0);
    for (const auto& c : s) {
        ++remaining[c - 'a'];
    }

    std::vector<bool> in_stack(k, false);
    std::string stk;
    for (const auto& c : s) {
        if (!in_stack[c - 'a']) {
            while (!stk.empty() && stk.back() > c && remaining[stk.back() - 'a']) {
                in_stack[stk.back() - 'a'] = false;
                stk.pop_back();
            }
            stk.push_back(c);
            in_stack[c - 'a'] = true;
        }
        --remaining[c - 'a'];
    }
    return stk;
}
```

### Rust

```rust
fn remove_duplicate_letters(s: &str) -> String {
    let k = 26usize;
    let mut remaining = vec![0i32; k];
    for b in s.bytes() {
        remaining[(b - b'a') as usize] += 1;
    }

    let mut in_stack = vec![false; k];
    let mut stk: Vec<u8> = Vec::new();
    for b in s.bytes() {
        let idx = (b - b'a') as usize;
        if !in_stack[idx] {
            while let Some(&last) = stk.last() {
                let last_idx = (last - b'a') as usize;
                if last > b && remaining[last_idx] > 0 {
                    in_stack[last_idx] = false;
                    stk.pop();
                } else {
                    break;
                }
            }
            stk.push(b);
            in_stack[idx] = true;
        }
        remaining[idx] -= 1;
    }
    String::from_utf8(stk).unwrap()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/remove-duplicate-letters.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
