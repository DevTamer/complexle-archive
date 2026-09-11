# Search in Rotated Sorted Array

**Puzzle date:** 2026-06-22  
**Category:** binary search  
**Time complexity:** `O(log n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the while loop, which performs a modified binary search on the array. Each iteration of the loop eliminates half of the remaining elements by moving either `lo` or `hi` to `mid ± 1`, so the loop runs at most log₂(n) times. You might be tempted to say O(n) because the array is rotated and seems like it might require a linear scan, but the key insight is that at every step you can still determine which half is sorted and whether the target lies within it, preserving the halving property. No additional data structures are used — only a fixed number of integer variables (`lo`, `hi`, `mid`) — so the space complexity is O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def search(nums: list[int], target: int) -> int:
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        if nums[lo] <= nums[mid]:
            if nums[lo] <= target < nums[mid]:
                hi = mid - 1
            else:
                lo = mid + 1
        else:
            if nums[mid] < target <= nums[hi]:
                lo = mid + 1
            else:
                hi = mid - 1
    return -1
```

### C++

```cpp
int search(std::vector<int>& nums, int target) {
    int lo = 0, hi = nums.size() - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] == target) return mid;
        if (nums[lo] <= nums[mid]) {
            if (nums[lo] <= target && target < nums[mid]) hi = mid - 1;
            else lo = mid + 1;
        } else {
            if (nums[mid] < target && target <= nums[hi]) lo = mid + 1;
            else hi = mid - 1;
        }
    }
    return -1;
}
```

### Rust

```rust
fn search(nums: &[i32], target: i32) -> i32 {
    let (mut lo, mut hi) = (0i32, nums.len() as i32 - 1);
    while lo <= hi {
        let mid = lo + (hi - lo) / 2;
        let m = nums[mid as usize];
        if m == target { return mid; }
        if nums[lo as usize] <= m {
            if nums[lo as usize] <= target && target < m { hi = mid - 1; }
            else { lo = mid + 1; }
        } else {
            if m < target && target <= nums[hi as usize] { lo = mid + 1; }
            else { hi = mid - 1; }
        }
    }
    -1
}
```

---

Played daily at [complexle.com](https://complexle.com).
