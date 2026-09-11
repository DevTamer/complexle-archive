# Valid Palindrome

**Puzzle date:** 2026-09-06  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The two pointers i and j move toward each other using a single while loop with two nested skip-loops, but together the inner loops only advance the pointers, never resetting them, so the total number of pointer movements across the whole run is bounded by n. This means every character is visited at most once overall, giving you O(n) time even though it looks like nested loops. The tempting O(n²) answer comes from seeing loops inside a loop, but since i and j only increase and decrease respectively without ever backtracking, the work doesn't multiply—it just adds up linearly. Space-wise, the algorithm only uses a fixed number of integer variables (i and j) and doesn't build any new strings or data structures, so it stays at O(1) regardless of input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def is_palindrome(s: str) -> bool:
    i, j = 0, len(s) - 1
    while i < j:
        while i < j and not s[i].isalnum():
            i += 1
        while i < j and not s[j].isalnum():
            j -= 1
        if s[i].lower() != s[j].lower():
            return False
        i, j = i + 1, j - 1
    return True
```

### C++

```cpp
bool isPalindrome(std::string s) {
    int i = 0, j = (int)s.length() - 1;
    while (i < j) {
        while (i < j && !isalnum((unsigned char)s[i])) i++;
        while (i < j && !isalnum((unsigned char)s[j])) j--;
        if (tolower((unsigned char)s[i]) != tolower((unsigned char)s[j])) return false;
        i++; j--;
    }
    return true;
}
```

### Rust

```rust
fn is_palindrome(s: &str) -> bool {
    let chars: Vec<char> = s.chars().collect();
    let mut i: i32 = 0;
    let mut j: i32 = chars.len() as i32 - 1;
    while i < j {
        while i < j && !chars[i as usize].is_alphanumeric() {
            i += 1;
        }
        while i < j && !chars[j as usize].is_alphanumeric() {
            j -= 1;
        }
        if chars[i as usize].to_ascii_lowercase() != chars[j as usize].to_ascii_lowercase() {
            return false;
        }
        i += 1;
        j -= 1;
    }
    true
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/valid-palindrome.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
