# 3Sum Closest

**Puzzle date:** 2026-09-04  
**Category:** two pointers  
**Time complexity:** `O(n^2)`  
**Space complexity:** `O(1)`

## Explanation

You have an outer loop over the array combined with an inner two-pointer loop, and this nested structure is what drives the cost. The sort takes O(n log n), but the outer for-loop runs O(n) times, and for each iteration the inner while loop with left/right pointers can also run up to O(n) times, giving O(n^2) total work which dominates the sort. A tempting wrong answer is O(n log n) because of the sort call, but that cost is dwarfed by the nested two-pointer scan that happens for every outer index. Space-wise, aside from the in-place sort, you only use a fixed number of variables like result, min_diff, left, and right, so the extra space used doesn't grow with input size, making it O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def three_sum_closest(nums: list[int], target: int) -> int:
    result, min_diff = 0, float("inf")
    nums.sort()
    for i in reversed(range(2, len(nums))):
        if i + 1 < len(nums) and nums[i] == nums[i + 1]:
            continue
        left, right = 0, i - 1
        while left < right:
            total = nums[left] + nums[right] + nums[i]
            if total < target:
                left += 1
            elif total > target:
                right -= 1
            else:
                return target
            if abs(total - target) < min_diff:
                min_diff = abs(total - target)
                result = total
    return result
```

### C++

```cpp
int threeSumClosest(std::vector<int>& nums, int target) {
    std::sort(nums.begin(), nums.end());
    int result = 0;
    int min_diff = INT_MAX;
    for (int i = (int)nums.size() - 1; i >= 2; --i) {
        if (i + 1 < (int)nums.size() && nums[i] == nums[i + 1]) {
            continue;
        }
        int left = 0, right = i - 1;
        while (left < right) {
            int total = nums[left] + nums[right] + nums[i];
            if (total < target) {
                ++left;
            } else if (total > target) {
                --right;
            } else {
                return target;
            }
            if (std::abs(total - target) < min_diff) {
                min_diff = std::abs(total - target);
                result = total;
            }
        }
    }
    return result;
}
```

### Rust

```rust
fn three_sum_closest(nums: &[i32], target: i32) -> i32 {
    let mut nums = nums.to_vec();
    nums.sort();
    let mut result = 0;
    let mut min_diff = i32::MAX;
    let n = nums.len();
    let mut i = n as i32 - 1;
    while i >= 2 {
        let ui = i as usize;
        if ui + 1 < n && nums[ui] == nums[ui + 1] {
            i -= 1;
            continue;
        }
        let mut left = 0usize;
        let mut right = ui - 1;
        while left < right {
            let total = nums[left] + nums[right] + nums[ui];
            if total < target {
                left += 1;
            } else if total > target {
                right -= 1;
            } else {
                return target;
            }
            if (total - target).abs() < min_diff {
                min_diff = (total - target).abs();
                result = total;
            }
        }
        i -= 1;
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/3sum-closest.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
