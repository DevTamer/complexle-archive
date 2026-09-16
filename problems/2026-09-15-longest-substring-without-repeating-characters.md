# Longest Substring Without Repeating Characters

**Puzzle date:** 2026-09-15  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(min(n, m))`

## Explanation

The single for loop iterates through the string once, and each iteration does constant-time work (a dictionary lookup and update, plus a couple of comparisons), so the dominant cost is that one pass over the n characters, giving you O(n) time. It's tempting to think O(n²) because sliding window problems often look like they need nested loops to check substrings, but here the 'left' pointer only moves forward and never rescans characters, avoiding that extra cost. For space, the lookup dictionary can grow to hold one entry per distinct character seen, so its size is bounded by either the string length n or the size of the character set m, whichever is smaller, giving O(min(n, m)). Thinking the space is O(1) is a common mistake since the code has no obvious large structure, but the dictionary does scale with unique input characters, so it's not truly constant.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def length_of_longest_substring(s: str) -> int:
    result, left = 0, 0
    lookup: dict[str, int] = {}
    for right, ch in enumerate(s):
        if ch in lookup:
            left = max(left, lookup[ch] + 1)
        lookup[ch] = right
        result = max(result, right - left + 1)
    return result
```

### C++

```cpp
int lengthOfLongestSubstring(std::string s) {
    int result = 0;
    std::unordered_map<char, int> lookup;
    for (int left = 0, right = 0; right < (int)s.length(); ++right) {
        if (lookup.count(s[right])) {
            left = std::max(left, lookup[s[right]] + 1);
        }
        lookup[s[right]] = right;
        result = std::max(result, right - left + 1);
    }
    return result;
}
```

### Rust

```rust
fn length_of_longest_substring(s: &str) -> i32 {
    let chars: Vec<char> = s.chars().collect();
    let mut result: i32 = 0;
    let mut left: i32 = 0;
    let mut lookup: HashMap<char, i32> = HashMap::new();
    for right in 0..chars.len() {
        let c = chars[right];
        if let Some(&idx) = lookup.get(&c) {
            left = left.max(idx + 1);
        }
        lookup.insert(c, right as i32);
        result = result.max(right as i32 - left + 1);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/longest-substring-without-repeating-characters.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
