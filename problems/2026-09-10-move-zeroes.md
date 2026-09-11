# Move Zeroes

**Puzzle date:** 2026-09-10  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The single for loop iterates through the list once, and inside the loop you only do a constant-time check and a swap, so the dominant cost is that one pass over n elements, giving O(n) time. There's no nested loop or recursion adding extra factors, which is why O(n log n) or O(n²) would overstate the work. The swap happens in place using existing indices, so no new lists, arrays, or recursive stacks are created, meaning space stays O(1) regardless of input size. The most tempting wrong answer, O(n) space, is incorrect because the function modifies the input list directly instead of allocating a new one proportional to n.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def move_zeroes(nums: list[int]) -> list[int]:
    pos = 0
    for i in range(len(nums)):
        if nums[i]:
            nums[i], nums[pos] = nums[pos], nums[i]
            pos += 1
    return nums
```

### C++

```cpp
#include <vector>
#include <utility>

std::vector<int> moveZeroes(std::vector<int>& nums) {
    int pos = 0;
    for (auto& num : nums) {
        if (num) {
            std::swap(nums[pos++], num);
        }
    }
    return nums;
}
```

### Rust

```rust
fn move_zeroes(nums: &mut Vec<i32>) -> Vec<i32> {
    let mut pos = 0;
    for i in 0..nums.len() {
        if nums[i] != 0 {
            nums.swap(i, pos);
            pos += 1;
        }
    }
    nums.clone()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/move-zeroes.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
