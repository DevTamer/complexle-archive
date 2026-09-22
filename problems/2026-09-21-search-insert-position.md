# Search Insert Position

**Puzzle date:** 2026-09-21  
**Category:** binary search  
**Time complexity:** `O(log n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the while loop that performs binary search, cutting the search range roughly in half each iteration by adjusting left and right. This halving behavior means the loop runs about log2(n) times before left exceeds right, giving you O(log n) time. You might be tempted to say O(n) because you're scanning an array, but this code never checks every element sequentially—it jumps to the middle and discards half the remaining range each time, unlike a linear scan. Space-wise, only a few variables (left, right, mid) are used regardless of input size, and no extra data structures or recursive call stacks are created, so the space complexity stays constant at O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def search_insert(nums: list[int], target: int) -> int:
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] >= target:
            right = mid - 1
        else:
            left = mid + 1
    return left
```

### C++

```cpp
int searchInsert(std::vector<int>& nums, int target) {
    int left = 0;
    int right = static_cast<int>(nums.size()) - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] >= target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

### Rust

```rust
fn search_insert(nums: &[i32], target: i32) -> i32 {
    let mut left: i32 = 0;
    let mut right: i32 = nums.len() as i32 - 1;

    while left <= right {
        let mid = left + (right - left) / 2;
        if nums[mid as usize] >= target {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }

    left
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/search-insert-position.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
