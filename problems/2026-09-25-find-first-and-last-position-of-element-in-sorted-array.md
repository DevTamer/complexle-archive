# Find First and Last Position of Element in Sorted Array

**Puzzle date:** 2026-09-25  
**Category:** binary search  
**Time complexity:** `O(log n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the two calls to binary_search, each of which halves the search range every iteration, giving O(log n) per call and O(log n) overall since two sequential O(log n) calls still sum to O(log n). You might be tempted to think O(n) because of the linear array, but the code never scans the array linearly; it only jumps to the middle index each time, discarding half the remaining range. Space stays O(1) because binary_search only uses a fixed number of integer variables (left, right, mid) regardless of input size, and the lambda closures don't allocate any additional per-element storage. No recursion or extra data structures are used, so no call stack growth or auxiliary arrays occur.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def search_range(nums: list[int], target: int) -> list[int]:
    def binary_search(n: int, check) -> int:
        left, right = 0, n - 1
        while left <= right:
            mid = left + (right - left) // 2
            if check(mid):
                right = mid - 1
            else:
                left = mid + 1
        return left

    left = binary_search(len(nums), lambda i: nums[i] >= target)
    if left == len(nums) or nums[left] != target:
        return [-1, -1]
    right = binary_search(len(nums), lambda i: nums[i] > target)
    return [left, right - 1]
```

### C++

```cpp
std::vector<int> searchRange(std::vector<int>& nums, int target) {
    auto binarySearch = [&](int n, std::function<bool(int)> check) -> int {
        int left = 0, right = n - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (check(mid)) right = mid - 1;
            else left = mid + 1;
        }
        return left;
    };

    int left = binarySearch((int)nums.size(), [&](int i) { return nums[i] >= target; });
    if (left == (int)nums.size() || nums[left] != target) return {-1, -1};
    int right = binarySearch((int)nums.size(), [&](int i) { return nums[i] > target; });
    return {left, right - 1};
}
```

### Rust

```rust
fn search_range(nums: &[i32], target: i32) -> Vec<i32> {
    fn binary_search<F: Fn(i32) -> bool>(n: i32, check: F) -> i32 {
        let mut left = 0;
        let mut right = n - 1;
        while left <= right {
            let mid = left + (right - left) / 2;
            if check(mid) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        left
    }

    let n = nums.len() as i32;
    let left = binary_search(n, |i| nums[i as usize] >= target);
    if left == n || nums[left as usize] != target {
        return vec![-1, -1];
    }
    let right = binary_search(n, |i| nums[i as usize] > target);
    vec![left, right - 1]
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/find-first-and-last-position-of-element-in-sorted-array.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
