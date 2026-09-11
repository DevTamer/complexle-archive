# House Robber

**Puzzle date:** 2026-06-29  
**Category:** dynamic programming  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single for-loop that iterates over every element in the nums list exactly once, giving you O(n) time. Each iteration does a constant amount of work (one max comparison and two variable assignments), so nothing inside the loop adds extra cost. You might be tempted to say O(n) space thinking a DP array is used, but notice that instead of storing all intermediate results in an array, this solution only keeps two variables (prev1 and prev2) at any time, which is constant O(1) space. The classic House Robber solution using a full dp array would be O(n) space, but this optimized version avoids that entirely.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def rob(nums: list[int]) -> int:
    prev2 = prev1 = 0
    for n in nums:
        curr = max(prev1, prev2 + n)
        prev2 = prev1
        prev1 = curr
    return prev1
```

### C++

```cpp
int rob(std::vector<int>& nums) {
    int prev2 = 0, prev1 = 0;
    for (int n : nums) {
        int curr = std::max(prev1, prev2 + n);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

### Rust

```rust
fn rob(nums: &[i32]) -> i32 {
    let mut prev2 = 0;
    let mut prev1 = 0;
    for &n in nums {
        let curr = prev1.max(prev2 + n);
        prev2 = prev1;
        prev1 = curr;
    }
    prev1
}
```

---

Played daily at [complexle.com](https://complexle.com).
