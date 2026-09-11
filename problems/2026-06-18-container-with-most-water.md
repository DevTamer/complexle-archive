# Container With Most Water

**Puzzle date:** 2026-06-18  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single while loop that moves two pointers (lo and hi) from opposite ends of the array toward each other. Each iteration advances at least one pointer by one step, so the loop runs at most n-1 times total, giving you O(n) time. The most tempting wrong answer is O(n²) — you might think there are two nested loops because there are two pointers, but they move independently toward each other rather than one being nested inside the other, so their combined work is still linear. For space, you only use a fixed number of variables (lo, hi, best, area) regardless of input size, so no extra memory scales with n, giving you O(1) space.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def max_area(height: list[int]) -> int:
    lo, hi = 0, len(height) - 1
    best = 0
    while lo < hi:
        area = (hi - lo) * min(height[lo], height[hi])
        best = max(best, area)
        if height[lo] < height[hi]:
            lo += 1
        else:
            hi -= 1
    return best
```

### C++

```cpp
#include <vector>
#include <algorithm>

int maxArea(std::vector<int>& height) {
    int lo = 0, hi = height.size() - 1, best = 0;
    while (lo < hi) {
        int area = (hi - lo) * std::min(height[lo], height[hi]);
        best = std::max(best, area);
        if (height[lo] < height[hi]) lo++;
        else hi--;
    }
    return best;
}
```

### Rust

```rust
fn max_area(height: &[i32]) -> i32 {
    let (mut lo, mut hi) = (0usize, height.len() - 1);
    let mut best = 0;
    while lo < hi {
        let area = (hi - lo) as i32 * height[lo].min(height[hi]);
        best = best.max(area);
        if height[lo] < height[hi] { lo += 1; }
        else { hi -= 1; }
    }
    best
}
```

---

Played daily at [complexle.com](https://complexle.com).
