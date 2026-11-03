# Remove All Adjacent Duplicates In String

**Puzzle date:** 2026-11-02  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

Each character of the string is appended to the result list at most once and popped at most once, so although the loop body can both push and pop, the total number of stack operations across the whole run is bounded by 2n. That amortised accounting gives O(n), and the final join is another linear pass. Space is O(n) because the result list can hold every character when no adjacent duplicates exist — for example a string with all distinct characters is copied in full — so the extra memory scales with the input rather than being constant.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def remove_duplicates(s: str) -> str:
    result = []
    for c in s:
        if result and result[-1] == c:
            result.pop()
        else:
            result.append(c)
    return "".join(result)
```

### C++

```cpp
std::string removeDuplicates(std::string s) {
    std::string result;
    for (char c : s) {
        if (!result.empty() && result.back() == c) {
            result.pop_back();
        } else {
            result.push_back(c);
        }
    }
    return result;
}
```

### Rust

```rust
fn remove_duplicates(s: &str) -> String {
    let mut result: Vec<char> = Vec::new();
    for c in s.chars() {
        if result.last() == Some(&c) {
            result.pop();
        } else {
            result.push(c);
        }
    }
    result.into_iter().collect()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/remove-all-adjacent-duplicates-in-string.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
