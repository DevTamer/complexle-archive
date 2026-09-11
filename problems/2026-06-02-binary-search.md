# Binary Search

**Puzzle date:** 2026-06-02  
**Category:** binary search  
**Time complexity:** `O(log n)`  
**Space complexity:** `O(1)`

## Explanation

Binary search halves the search space on each iteration, so the number of iterations is at most log₂(n), yielding O(log n) time complexity. The algorithm uses only a fixed number of variables (lo, hi, mid) regardless of input size, so space complexity is O(1). No recursion or auxiliary data structures are used, confirming constant space usage.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def binary_search(nums: list[int], target: int) -> int:
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1
    return -1
```

### C++

```cpp
#include <vector>

int binarySearch(std::vector<int>& nums, int target) {
    int lo = 0, hi = nums.size() - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```

### Rust

```rust
fn binary_search(nums: &[i32], target: i32) -> i32 {
    let (mut lo, mut hi) = (0i32, nums.len() as i32 - 1);
    while lo <= hi {
        let mid = lo + (hi - lo) / 2;
        match nums[mid as usize].cmp(&target) {
            std::cmp::Ordering::Equal => return mid,
            std::cmp::Ordering::Less => lo = mid + 1,
            std::cmp::Ordering::Greater => hi = mid - 1,
        }
    }
    -1
}
```

---

Played daily at [complexle.com](https://complexle.com).
