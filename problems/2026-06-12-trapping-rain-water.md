# Trapping Rain Water

**Puzzle date:** 2026-06-12  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The two-pointer approach traverses the height array exactly once, with lo starting at the left and hi starting at the right, each moving inward until they meet — giving O(n) time. Only a fixed number of scalar variables (lo, hi, max_left, max_right, water) are used regardless of input size, resulting in O(1) space complexity.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def trap(height: list[int]) -> int:
    if not height:
        return 0
    lo, hi = 0, len(height) - 1
    max_left = max_right = water = 0
    while lo < hi:
        if height[lo] < height[hi]:
            if height[lo] >= max_left:
                max_left = height[lo]
            else:
                water += max_left - height[lo]
            lo += 1
        else:
            if height[hi] >= max_right:
                max_right = height[hi]
            else:
                water += max_right - height[hi]
            hi -= 1
    return water
```

### C++

```cpp
#include <vector>

int trap(std::vector<int>& height) {
    if (height.empty()) return 0;
    int lo = 0, hi = height.size() - 1;
    int maxLeft = 0, maxRight = 0, water = 0;
    while (lo < hi) {
        if (height[lo] < height[hi]) {
            if (height[lo] >= maxLeft) maxLeft = height[lo];
            else water += maxLeft - height[lo];
            lo++;
        } else {
            if (height[hi] >= maxRight) maxRight = height[hi];
            else water += maxRight - height[hi];
            hi--;
        }
    }
    return water;
}
```

### Rust

```rust
fn trap(height: &[i32]) -> i32 {
    if height.is_empty() { return 0; }
    let (mut lo, mut hi) = (0, height.len() - 1);
    let (mut max_left, mut max_right, mut water) = (0, 0, 0);
    while lo < hi {
        if height[lo] < height[hi] {
            if height[lo] >= max_left { max_left = height[lo]; }
            else { water += max_left - height[lo]; }
            lo += 1;
        } else {
            if height[hi] >= max_right { max_right = height[hi]; }
            else { water += max_right - height[hi]; }
            hi -= 1;
        }
    }
    water
}
```

---

Played daily at [complexle.com](https://complexle.com).
