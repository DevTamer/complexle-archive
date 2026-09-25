# Minimum Size Subarray Sum

**Puzzle date:** 2026-09-24  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

You have a sliding window here: the outer for-loop advances i once per element, and the inner while-loop advances start, but start only ever moves forward and never resets. That means across the whole run, start can only increment n times total, so the two loops together do at most 2n steps, giving you O(n) overall. This is why it's not O(n²): even though there's a loop inside a loop, the inner loop's total work is bounded by n across all outer iterations, not n per outer iteration, since both pointers only move in one direction. For space, you're only tracking a few scalar variables (start, total, min_size, i, n), not any structure that grows with input size, so space stays O(1) regardless of how big nums is.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def min_sub_array_len(s: int, nums: list[int]) -> int:
    start = 0
    total = 0
    min_size = float("inf")
    for i, n in enumerate(nums):
        total += n
        while total >= s:
            min_size = min(min_size, i - start + 1)
            total -= nums[start]
            start += 1
    return min_size if min_size != float("inf") else 0
```

### C++

```cpp
int minSubArrayLen(int s, std::vector<int>& nums) {
    int start = -1, sum = 0, min_size = std::numeric_limits<int>::max();
    for (int i = 0; i < (int)nums.size(); ++i) {
        sum += nums[i];
        while (sum >= s) {
            min_size = std::min(min_size, i - start);
            sum -= nums[++start];
        }
    }
    if (min_size == std::numeric_limits<int>::max()) {
        return 0;
    }
    return min_size;
}
```

### Rust

```rust
fn min_sub_array_len(s: i32, nums: &[i32]) -> i32 {
    let mut start: i32 = 0;
    let mut sum: i32 = 0;
    let mut min_size = i32::MAX;
    for i in 0..nums.len() {
        sum += nums[i];
        while sum >= s {
            min_size = min_size.min(i as i32 - start + 1);
            sum -= nums[start as usize];
            start += 1;
        }
    }
    if min_size == i32::MAX { 0 } else { min_size }
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/minimum-size-subarray-sum.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
