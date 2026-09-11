# Sort Colors

**Puzzle date:** 2026-09-05  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the single while loop in tri_partition, where the pointer i moves from 0 up to right, and right can only decrease, so the loop body runs a bounded number of times proportional to the length of nums, giving you O(n). You might be tempted to think of this like a sorting algorithm and assume O(n log n), but this isn't a comparison sort over the whole range of values—it's a one-pass Dutch national flag partition that only ever compares each element to a fixed target and swaps it into place, so no nested loops or recursive splitting occur. Space-wise, the function only uses a few integer variables (i, left, right) and swaps elements in place within the original list, so no extra data structures that scale with n are created, making space O(1). The n distractor for space is tempting because sorting algorithms sometimes need auxiliary arrays or recursion stacks, but this in-place swap-based approach avoids that entirely.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def sort_colors(nums: list[int]) -> list[int]:
    def tri_partition(nums: list[int], target: int) -> None:
        i, left, right = 0, 0, len(nums) - 1
        while i <= right:
            if nums[i] > target:
                nums[i], nums[right] = nums[right], nums[i]
                right -= 1
            else:
                if nums[i] < target:
                    nums[left], nums[i] = nums[i], nums[left]
                    left += 1
                i += 1

    tri_partition(nums, 1)
    return nums
```

### C++

```cpp
std::vector<int> sortColors(std::vector<int>& nums) {
    const int target = 1;
    int right = static_cast<int>(nums.size()) - 1;
    for (int i = 0, left = 0; i <= right;) {
        if (nums[i] > target) {
            std::swap(nums[i], nums[right--]);
        } else {
            if (nums[i] < target) {
                std::swap(nums[left++], nums[i]);
            }
            ++i;
        }
    }
    return nums;
}
```

### Rust

```rust
fn sort_colors(nums: &mut [i32]) -> Vec<i32> {
    let target = 1;
    let mut i: isize = 0;
    let mut left: isize = 0;
    let mut right: isize = nums.len() as isize - 1;
    while i <= right {
        let ui = i as usize;
        if nums[ui] > target {
            nums.swap(ui, right as usize);
            right -= 1;
        } else {
            if nums[ui] < target {
                nums.swap(left as usize, ui);
                left += 1;
            }
            i += 1;
        }
    }
    nums.to_vec()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/sort-colors.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
