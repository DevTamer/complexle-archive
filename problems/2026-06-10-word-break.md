# Word Break

**Puzzle date:** 2026-06-10  
**Category:** dynamic programming  
**Time complexity:** `O(n³)`  
**Space complexity:** `O(n + m)`

## Explanation

The double loop over i and j gives O(n²) iterations, and each iteration performs a substring slice s[j:i] which takes O(n) time in the worst case, resulting in O(n³) total time. The space complexity is O(n + m) where n is the length of s for the dp array and m is the total number of characters in word_dict stored in the hash set (word_set).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def word_break(s: str, word_dict: list[str]) -> bool:
    word_set = set(word_dict)
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True
    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break
    return dp[n]
```

### C++

```cpp
bool wordBreak(std::string s, std::vector<std::string>& wordDict) {
    std::unordered_set<std::string> words(wordDict.begin(), wordDict.end());
    int n = s.size();
    std::vector<bool> dp(n + 1, false);
    dp[0] = true;
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j < i; j++) {
            if (dp[j] && words.count(s.substr(j, i - j))) {
                dp[i] = true;
                break;
            }
        }
    }
    return dp[n];
}
```

### Rust

```rust
fn word_break(s: &str, word_dict: &[&str]) -> bool {
    let words: HashSet<&str> = word_dict.iter().copied().collect();
    let n = s.len();
    let mut dp = vec![false; n + 1];
    dp[0] = true;
    for i in 1..=n {
        for j in 0..i {
            if dp[j] && words.contains(&s[j..i]) {
                dp[i] = true;
                break;
            }
        }
    }
    dp[n]
}
```

---

Played daily at [complexle.com](https://complexle.com).
