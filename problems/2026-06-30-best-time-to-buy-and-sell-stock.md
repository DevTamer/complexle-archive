# Best Time to Buy and Sell Stock

**Puzzle date:** 2026-06-30  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single `for p in prices` loop, which visits every element in the list exactly once. Because each iteration does only constant-time work — two comparisons and two assignments — the total time scales linearly with the number of prices, giving O(n). You might be tempted to guess O(n²) thinking that tracking a running minimum somehow implies a nested scan, but `min_price` is updated in place so no inner loop exists. For space, the algorithm uses only two scalar variables (`min_price` and `best`) regardless of how large the input list is, so extra memory usage is O(1) — it never grows with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def max_profit(prices: list[int]) -> int:
    min_price = float('inf')
    best = 0
    for p in prices:
        min_price = min(min_price, p)
        best = max(best, p - min_price)
    return best
```

### C++

```cpp
#include <vector>
#include <algorithm>
#include <limits>

int maxProfit(std::vector<int>& prices) {
    int minPrice = std::numeric_limits<int>::max();
    int best = 0;
    for (int p : prices) {
        minPrice = std::min(minPrice, p);
        best = std::max(best, p - minPrice);
    }
    return best;
}
```

### Rust

```rust
fn max_profit(prices: &[i32]) -> i32 {
    let mut min_price = i32::MAX;
    let mut best = 0;
    for &p in prices {
        min_price = min_price.min(p);
        best = best.max(p - min_price);
    }
    best
}
```

---

Played daily at [complexle.com](https://complexle.com).
