# Maximum Product Subarray

**Puzzle date:** 2026-07-16  
**Category:** dynamic programming  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single for-loop that iterates over nums[1:], visiting each element exactly once. Inside the loop, every operation — the swap, the max/min calls, and the result update — runs in constant time, so the total work scales linearly with the length of the input array. You might be tempted to think the max() and min() calls add extra complexity, but they each compare only two values, making them O(1) regardless of n. For space, you only maintain a fixed set of scalar variables (result, cur_max, cur_min) no matter how large the input is, so no additional memory proportional to n is ever allocated.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def max_product(nums: list[int]) -> int:
    result = nums[0]
    cur_max = cur_min = nums[0]
    for n in nums[1:]:
        if n < 0:
            cur_max, cur_min = cur_min, cur_max
        cur_max = max(n, cur_max * n)
        cur_min = min(n, cur_min * n)
        result = max(result, cur_max)
    return result
```

### C++

```cpp
#include <vector>
#include <algorithm>
#include <utility>

int maxProduct(std::vector<int>& nums) {
    int result = nums[0];
    int curMax = nums[0], curMin = nums[0];
    for (size_t i = 1; i < nums.size(); i++) {
        int n = nums[i];
        if (n < 0) std::swap(curMax, curMin);
        curMax = std::max(n, curMax * n);
        curMin = std::min(n, curMin * n);
        result = std::max(result, curMax);
    }
    return result;
}
```

### Rust

```rust
fn max_product(nums: &[i32]) -> i32 {
    let mut result = nums[0];
    let (mut cur_max, mut cur_min) = (nums[0], nums[0]);
    for &n in &nums[1..] {
        if n < 0 {
            std::mem::swap(&mut cur_max, &mut cur_min);
        }
        cur_max = n.max(cur_max * n);
        cur_min = n.min(cur_min * n);
        result = result.max(cur_max);
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
