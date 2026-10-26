# Find Minimum in Rotated Sorted Array

**Puzzle date:** 2026-10-25  
**Category:** binary search  
**Time complexity:** `O(log n)`  
**Space complexity:** `O(1)`

## Explanation

The while loop is a binary search: each iteration discards half the remaining range by moving either left or right to mid, so the number of iterations is log base 2 of n. Every operation inside the loop — computing mid, one comparison, one assignment — is constant time, giving O(log n) overall. It is tempting to answer O(n) because the array is rotated and therefore not fully sorted, but the comparison against nums[-1] is enough to tell which half contains the minimum, so no linear scan is ever needed. The space complexity is O(1): only the left, right, mid, and target integers are allocated, and this binary search is written iteratively, so there is no recursion stack that would push it to O(log n).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def find_min(nums: list[int]) -> int:
    left, right = 0, len(nums)
    target = nums[-1]

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] <= target:
            right = mid
        else:
            left = mid + 1

    return nums[left]
```

### C++

```cpp
int findMin(std::vector<int>& nums) {
    int left = 0, right = nums.size();
    int target = nums.back();

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] <= target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return nums[left];
}
```

### Rust

```rust
fn find_min(nums: &[i32]) -> i32 {
    let mut left = 0usize;
    let mut right = nums.len();
    let target = nums[nums.len() - 1];

    while left < right {
        let mid = left + (right - left) / 2;

        if nums[mid] <= target {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    nums[left]
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/find-minimum-in-rotated-sorted-array.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
