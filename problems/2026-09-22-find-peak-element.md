# Find Peak Element

**Puzzle date:** 2026-09-22  
**Category:** binary search  
**Time complexity:** `O(log n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the binary search loop that halves the search range (right - left) every iteration by comparing nums[mid] to nums[mid+1]. Because the range shrinks by half each time instead of moving one step at a time, you only need about log n iterations to converge on a peak, giving O(log n) time. The tempting wrong answer O(n) comes from assuming you scan every element like a linear search, but this code never does that since it discards half the remaining candidates each step. Space stays O(1) because the function only tracks a handful of integer variables (left, right, mid) and never allocates any extra arrays or recursive call stacks that would grow with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def find_peak_element(nums: list[int]) -> int:
    left, right = 0, len(nums) - 1
    while left < right:
        mid = left + (right - left) // 2
        if nums[mid] > nums[mid + 1]:
            right = mid
        else:
            left = mid + 1
    return left
```

### C++

```cpp
int findPeakElement(std::vector<int>& nums) {
    int left = 0, right = static_cast<int>(nums.size()) - 1;

    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] > nums[mid + 1]) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

### Rust

```rust
fn find_peak_element(nums: &[i32]) -> i32 {
    let mut left: i32 = 0;
    let mut right: i32 = nums.len() as i32 - 1;

    while left < right {
        let mid = left + (right - left) / 2;
        if nums[mid as usize] > nums[(mid + 1) as usize] {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    left
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/find-peak-element.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
