# Climbing Stairs

**Puzzle date:** 2026-06-04  
**Category:** dynamic programming  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The function iterates from 3 to n+1 exactly once, performing constant-time operations in each iteration, resulting in O(n) time complexity. Only two variables (a and b) are used regardless of input size, so the space complexity is O(1) — no arrays or recursive call stack are involved.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def climb_stairs(n: int) -> int:
    if n <= 2:
        return n
    a, b = 1, 2
    for _ in range(3, n + 1):
        a, b = b, a + b
    return b
```

### C++

```cpp
int climbStairs(int n) {
    if (n <= 2) return n;
    int a = 1, b = 2;
    for (int i = 3; i <= n; i++) {
        int tmp = b;
        b = a + b;
        a = tmp;
    }
    return b;
}
```

### Rust

```rust
fn climb_stairs(n: u32) -> u64 {
    if n <= 2 { return n as u64; }
    let (mut a, mut b) = (1u64, 2u64);
    for _ in 3..=n {
        let tmp = b;
        b = a + b;
        a = tmp;
    }
    b
}
```

---

Played daily at [complexle.com](https://complexle.com).
