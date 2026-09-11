# Valid Parentheses

**Puzzle date:** 2026-06-05  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The algorithm iterates through each character in the string exactly once, performing O(1) operations per character (dictionary lookup, stack push/pop), resulting in O(n) time complexity where n is the length of the string. The space complexity is O(n) in the worst case because the stack can grow up to n/2 elements (e.g., when all characters are opening brackets like '((((...'), and the mapping dictionary is constant size O(1) so it does not affect the overall space complexity.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def is_valid(s: str) -> bool:
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    for ch in s:
        if ch in mapping:
            top = stack.pop() if stack else '#'
            if mapping[ch] != top:
                return False
        else:
            stack.append(ch)
    return not stack
```

### C++

```cpp
bool isValid(std::string s) {
    std::stack<char> stk;
    std::unordered_map<char,char> m = {{')', '('}, {'}', '{'}, {']', '['}};
    for (char ch : s) {
        if (m.count(ch)) {
            char top = stk.empty() ? '#' : stk.top();
            if (!stk.empty()) stk.pop();
            if (m[ch] != top) return false;
        } else {
            stk.push(ch);
        }
    }
    return stk.empty();
}
```

### Rust

```rust
fn is_valid(s: &str) -> bool {
    let mut stack = Vec::new();
    for ch in s.chars() {
        match ch {
            '(' | '{' | '[' => stack.push(ch),
            ')' => if stack.pop() != Some('(') { return false; },
            '}' => if stack.pop() != Some('{') { return false; },
            ']' => if stack.pop() != Some('[') { return false; },
            _ => {}
        }
    }
    stack.is_empty()
}
```

---

Played daily at [complexle.com](https://complexle.com).
