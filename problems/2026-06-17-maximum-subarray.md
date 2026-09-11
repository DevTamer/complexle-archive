# Maximum Subarray

**Puzzle date:** 2026-06-17  
**Category:** dynamic programming  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single for-loop that iterates over nums[1:], visiting each element exactly once. Because each iteration does only a constant amount of work (two max() comparisons and an addition), the total time scales linearly with the input size n. You might be tempted to say O(n²) if you imagined tracking subarrays explicitly, but Kadane's algorithm cleverly avoids that by carrying a running sum in 'curr', meaning no nested loops are needed. For space, only two scalar variables ('best' and 'curr') are used regardless of how large the input is, so the extra memory stays constant at O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def max_subarray(nums: list[int]) -> int:
    best = curr = nums[0]
    for n in nums[1:]:
        curr = max(n, curr + n)
        best = max(best, curr)
    return best
```

### C++

```cpp
int maxSubArray(std::vector<int>& nums) {
    int best = nums[0], curr = nums[0];
    for (size_t i = 1; i < nums.size(); i++) {
        curr = std::max(nums[i], curr + nums[i]);
        best = std::max(best, curr);
    }
    return best;
}
```

### Rust

```rust
fn max_subarray(nums: &[i32]) -> i32 {
    let mut best = nums[0];
    let mut curr = nums[0];
    for &n in &nums[1..] {
        curr = n.max(curr + n);
        best = best.max(curr);
    }
    best
}
```

---

Played daily at [complexle.com](https://complexle.com).
