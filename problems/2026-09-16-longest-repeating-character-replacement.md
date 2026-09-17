# Longest Repeating Character Replacement

**Puzzle date:** 2026-09-16  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

You just need to look at the single for loop iterating over the string once with index i from 0 to len(s)-1, doing constant-time work (dictionary updates and comparisons) each iteration, which gives you O(n). It's tempting to think O(n^2) because of the sliding window pattern, but the window never actually shrinks in a nested loop fashion here—result only increases or stays the same, so there's no repeated re-scanning. For space, the Counter dictionary only ever holds counts for distinct characters, and since this problem deals with a bounded alphabet (like lowercase letters), that count stays effectively constant regardless of input size, giving O(1) space. You might think O(n) space because a Counter could grow with input, but here it's bounded by the alphabet size, not the string length.”

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def character_replacement(s: str, k: int) -> int:
    from collections import Counter
    result, max_count = 0, 0
    count = Counter()
    for i in range(len(s)):
        count[s[i]] += 1
        max_count = max(max_count, count[s[i]])
        if result - max_count >= k:
            count[s[i - result]] -= 1
        else:
            result += 1
    return result
```

### C++

```cpp
int characterReplacement(std::string s, int k) {
    int result = 0, max_count = 0;
    std::unordered_map<char, int> count;
    for (int i = 0; i < (int)s.length(); ++i) {
        ++count[s[i]];
        max_count = std::max(max_count, count[s[i]]);
        if (result - max_count >= k) {
            --count[s[i - result]];
        } else {
            ++result;
        }
    }
    return result;
}
```

### Rust

```rust
fn character_replacement(s: &str, k: i32) -> i32 {
    let chars: Vec<char> = s.chars().collect();
    let mut result: i32 = 0;
    let mut max_count: i32 = 0;
    let mut count: HashMap<char, i32> = HashMap::new();
    for i in 0..chars.len() {
        let c = chars[i];
        let entry = count.entry(c).or_insert(0);
        *entry += 1;
        max_count = max_count.max(*entry);
        if result - max_count >= k {
            let idx = (i as i32 - result) as usize;
            let rc = chars[idx];
            if let Some(e) = count.get_mut(&rc) {
                *e -= 1;
            }
        } else {
            result += 1;
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/longest-repeating-character-replacement.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
