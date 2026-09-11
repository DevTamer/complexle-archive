# Squares of a Sorted Array

**Puzzle date:** 2026-09-07  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the while loop that merges the negative and non-negative portions of the array, and each iteration does constant work while advancing either the left or right pointer by one. Since the two pointers together traverse every element of nums exactly once, the loop runs O(n) times, and the initial bisect_left call only costs O(log n) which is dwarfed by the linear merge. You might be tempted to say O(log n) because of the bisect call, but that only finds the split point—it does not account for building the full result array. The result list you build and return holds n squared values, so space is O(n), not O(1), even though you only use a couple of extra pointer variables besides that list.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
import bisect

def sorted_squares(nums: list[int]) -> list[int]:
    right = bisect.bisect_left(nums, 0)
    left = right - 1
    result = []
    while left >= 0 or right < len(nums):
        if right == len(nums) or (left >= 0 and nums[left] ** 2 < nums[right] ** 2):
            result.append(nums[left] ** 2)
            left -= 1
        else:
            result.append(nums[right] ** 2)
            right += 1
    return result
```

### C++

```cpp
#include <vector>
#include <algorithm>

std::vector<int> sortedSquares(std::vector<int>& nums) {
    int right = std::distance(nums.cbegin(), std::lower_bound(nums.cbegin(), nums.cend(), 0));
    int left = right - 1;
    std::vector<int> result;
    while (left >= 0 || right < (int)nums.size()) {
        if (right == (int)nums.size() || (left >= 0 && nums[left] * nums[left] < nums[right] * nums[right])) {
            result.push_back(nums[left] * nums[left]);
            left--;
        } else {
            result.push_back(nums[right] * nums[right]);
            right++;
        }
    }
    return result;
}
```

### Rust

```rust
fn sorted_squares(nums: &[i32]) -> Vec<i32> {
    let right0 = nums.partition_point(|&x| x < 0);
    let mut right: i64 = right0 as i64;
    let mut left: i64 = right - 1;
    let n = nums.len() as i64;
    let mut result = Vec::new();
    while left >= 0 || right < n {
        if right == n || (left >= 0 && nums[left as usize] * nums[left as usize] < nums[right as usize] * nums[right as usize]) {
            result.push(nums[left as usize] * nums[left as usize]);
            left -= 1;
        } else {
            result.push(nums[right as usize] * nums[right as usize]);
            right += 1;
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/squares-of-a-sorted-array.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
