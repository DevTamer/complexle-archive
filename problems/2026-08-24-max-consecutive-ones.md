# Max Consecutive Ones

**Puzzle date:** 2026-08-24  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The single for loop that walks through nums is what drives the cost here, since you touch each element exactly once to update local_max and result. Because there's no nesting, recursion, or repeated scanning of the list, the work grows in direct proportion to the number of elements, giving you O(n) time. A tempting wrong answer is O(n²), but that would only apply if you had a nested loop or repeated inner scan for each element, which this code does not do. For space, you only ever store two integer variables, result and local_max, regardless of how large nums is, so the space stays constant at O(1) instead of growing with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def find_max_consecutive_ones(nums: list[int]) -> int:
    result, local_max = 0, 0
    for n in nums:
        local_max = local_max + 1 if n else 0
        result = max(result, local_max)
    return result
```

### C++

```cpp
#include <vector>
#include <algorithm>

int findMaxConsecutiveOnes(std::vector<int>& nums) {
    int result = 0, local_max = 0;
    for (const auto& n : nums) {
        local_max = n ? local_max + 1 : 0;
        result = std::max(result, local_max);
    }
    return result;
}
```

### Rust

```rust
fn find_max_consecutive_ones(nums: &[i32]) -> i32 {
    let mut result = 0;
    let mut local_max = 0;
    for &n in nums.iter() {
        local_max = if n != 0 { local_max + 1 } else { 0 };
        result = std::cmp::max(result, local_max);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/max-consecutive-ones.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
