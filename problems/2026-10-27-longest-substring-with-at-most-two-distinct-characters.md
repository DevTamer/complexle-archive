# Longest Substring with At Most Two Distinct Characters

**Puzzle date:** 2026-10-27  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

Although there is a while loop nested inside the for loop, this is a sliding window: start only ever moves forward, and across the entire run it advances at most n times in total. Each character is therefore added once and removed at most once, giving O(n) amortized rather than the O(n²) the nested loops suggest at a glance. The space complexity is the interesting part: visited is a fixed array of 256 counters, sized by the character set rather than by the input, so it does not grow with n. That makes the extra space O(1) even though the array looks large — a common trap is to call it O(n) because it is a list.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def length_of_longest_substring_two_distinct(s: str) -> int:
    longest, start, distinct_count = 0, 0, 0
    visited = [0] * 256
    for i, char in enumerate(s):
        if visited[ord(char)] == 0:
            distinct_count += 1
        visited[ord(char)] += 1
        while distinct_count > 2:
            visited[ord(s[start])] -= 1
            if visited[ord(s[start])] == 0:
                distinct_count -= 1
            start += 1
        longest = max(longest, i - start + 1)
    return longest
```

### C++

```cpp
int lengthOfLongestSubstringTwoDistinct(const std::string& s) {
    int longest = 0, start = 0, distinct_count = 0;
    std::array<int, 256> visited = {0};
    for (int i = 0; i < (int)s.length(); ++i) {
        if (visited[(unsigned char)s[i]] == 0) {
            ++distinct_count;
        }
        ++visited[(unsigned char)s[i]];
        while (distinct_count > 2) {
            --visited[(unsigned char)s[start]];
            if (visited[(unsigned char)s[start]] == 0) {
                --distinct_count;
            }
            ++start;
        }
        longest = std::max(longest, i - start + 1);
    }
    return longest;
}
```

### Rust

```rust
fn length_of_longest_substring_two_distinct(s: &str) -> i32 {
    let bytes = s.as_bytes();
    let mut longest = 0i32;
    let mut start = 0usize;
    let mut distinct_count = 0i32;
    let mut visited = [0i32; 256];
    for i in 0..bytes.len() {
        let c = bytes[i] as usize;
        if visited[c] == 0 {
            distinct_count += 1;
        }
        visited[c] += 1;
        while distinct_count > 2 {
            let sc = bytes[start] as usize;
            visited[sc] -= 1;
            if visited[sc] == 0 {
                distinct_count -= 1;
            }
            start += 1;
        }
        longest = longest.max((i - start + 1) as i32);
    }
    longest
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/longest-substring-with-at-most-two-distinct-characters.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
