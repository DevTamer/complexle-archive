# Coin Change

**Puzzle date:** 2026-06-20  
**Category:** dynamic programming  
**Time complexity:** `O(amount * n)`  
**Space complexity:** `O(amount)`

## Explanation

The dominant cost comes from the two nested loops: the outer loop runs `amount` times (from 1 to amount), and the inner loop iterates over all `n` coins for each value of i, giving you O(amount * n) total work. The `if c <= i` check is just a constant-time guard inside the inner loop and does not reduce the asymptotic cost. You might be tempted to say O(amount²) because the outer loop runs `amount` times, but the inner loop iterates over `n` coins — not `amount` values — so the second dimension is the number of coins, not the amount. The dp array is the only significant data structure allocated, and it has exactly `amount + 1` entries, so space is O(amount) regardless of how many coins there are.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def coin_change(coins: list[int], amount: int) -> int:
    dp = [amount + 1] * (amount + 1)
    dp[0] = 0
    for i in range(1, amount + 1):
        for c in coins:
            if c <= i:
                dp[i] = min(dp[i], dp[i - c] + 1)
    return dp[amount] if dp[amount] <= amount else -1
```

### C++

```cpp
int coinChange(std::vector<int>& coins, int amount) {
    std::vector<int> dp(amount + 1, amount + 1);
    dp[0] = 0;
    for (int i = 1; i <= amount; i++) {
        for (int c : coins) {
            if (c <= i)
                dp[i] = std::min(dp[i], dp[i - c] + 1);
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}
```

### Rust

```rust
fn coin_change(coins: &[i32], amount: i32) -> i32 {
    let n = amount as usize;
    let mut dp = vec![amount + 1; n + 1];
    dp[0] = 0;
    for i in 1..=n {
        for &c in coins {
            if c as usize <= i {
                dp[i] = dp[i].min(dp[i - c as usize] + 1);
            }
        }
    }
    if dp[n] > amount { -1 } else { dp[n] }
}
```

---

Played daily at [complexle.com](https://complexle.com).
