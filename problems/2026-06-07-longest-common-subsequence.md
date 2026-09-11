# Longest Common Subsequence

**Puzzle date:** 2026-06-07  
**Category:** dynamic programming  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(m*n)`

## Explanation

The algorithm uses two nested loops, one iterating over all m characters of text1 and one over all n characters of text2, resulting in O(m*n) time complexity. The space complexity is also O(m*n) because a 2D DP table of size (m+1)*(n+1) is allocated to store intermediate LCS lengths. Note that space could be optimized to O(min(m,n)) by using rolling arrays, but this implementation does not do that.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def lcs(text1: str, text2: str) -> int:
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    return dp[m][n]
```

### C++

```cpp
int lcs(std::string text1, std::string text2) {
    int m = text1.size(), n = text2.size();
    std::vector<std::vector<int>> dp(m + 1, std::vector<int>(n + 1, 0));
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1[i-1] == text2[j-1])
                dp[i][j] = dp[i-1][j-1] + 1;
            else
                dp[i][j] = std::max(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m][n];
}
```

### Rust

```rust
fn lcs(text1: &str, text2: &str) -> usize {
    let (a, b): (Vec<char>, Vec<char>) =
        (text1.chars().collect(), text2.chars().collect());
    let (m, n) = (a.len(), b.len());
    let mut dp = vec![vec![0usize; n + 1]; m + 1];
    for i in 1..=m {
        for j in 1..=n {
            dp[i][j] = if a[i-1] == b[j-1] {
                dp[i-1][j-1] + 1
            } else {
                dp[i-1][j].max(dp[i][j-1])
            };
        }
    }
    dp[m][n]
}
```

---

Played daily at [complexle.com](https://complexle.com).
