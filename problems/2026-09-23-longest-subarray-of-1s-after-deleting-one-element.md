# Longest Subarray of 1's After Deleting One Element

**Puzzle date:** 2026-09-23  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The single for loop drives the cost here, and it runs once through the array with the 'right' pointer, while 'left' only moves forward and never resets, so each index is touched a constant number of times overall. This sliding window pattern means the total work is proportional to the length of nums, giving you O(n) time. You might be tempted to think nested-loop behavior (O(n^2)) is happening because there's a pointer adjustment inside the loop, but since 'left' never goes backward, it doesn't restart or nest another full pass over the array. Space-wise, you only use a fixed number of scalar variables (count, left, right) regardless of input size, so no extra memory grows with n, making it O(1) space.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def longest_subarray(nums: list[int]) -> int:
    count, left = 0, 0
    right = 0
    for right in range(len(nums)):
        count += (nums[right] == 0)
        if count >= 2:
            count -= (nums[left] == 0)
            left += 1
    return (right - left + 1) - 1
```

### C++

```cpp
int longestSubarray(std::vector<int>& nums) {
    int count = 0, left = 0, right = 0;
    for (; right < (int)nums.size(); ++right) {
        count += (nums[right] == 0);
        if (count >= 2) {
            count -= (nums[left++] == 0);
        }
    }
    return (right - left) - 1;
}
```

### Rust

```rust
fn longest_subarray(nums: &[i32]) -> i32 {
    let mut count: i32 = 0;
    let mut left: usize = 0;
    let mut right: usize = 0;
    for r in 0..nums.len() {
        right = r;
        count += (nums[r] == 0) as i32;
        if count >= 2 {
            count -= (nums[left] == 0) as i32;
            left += 1;
        }
    }
    (right as i32 - left as i32 + 1) - 1
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/longest-subarray-of-1s-after-deleting-one-element.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
