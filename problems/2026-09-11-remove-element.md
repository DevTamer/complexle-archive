# Remove Element

**Puzzle date:** 2026-09-11  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the single while loop, where two pointers 'i' and 'last' move toward each other, each element being visited at most once before the loop ends. You might think swapping counts as extra nested work like a sort would, but each swap is a constant-time operation, so it doesn't add another loop layer, ruling out O(n²). Since there's no recursion or nested iteration, and the array is modified in place using only a couple of integer variables, the space usage stays constant regardless of input size. The O(n) space distractor might tempt you if you assume a new array is created, but this code swaps values directly in the original list without allocating extra storage.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def remove_element(nums: list[int], val: int) -> int:
    i, last = 0, len(nums) - 1
    while i <= last:
        if nums[i] == val:
            nums[i], nums[last] = nums[last], nums[i]
            last -= 1
        else:
            i += 1
    return last + 1
```

### C++

```cpp
int removeElement(std::vector<int>& nums, int val) {
    int left = 0, right = static_cast<int>(nums.size()) - 1;
    while (left <= right) {
        if (nums[left] == val) {
            std::swap(nums[left], nums[right]);
            --right;
        } else {
            ++left;
        }
    }
    return right + 1;
}
```

### Rust

```rust
fn remove_element(nums: &mut Vec<i32>, val: i32) -> i32 {
    let mut i: i32 = 0;
    let mut last: i32 = nums.len() as i32 - 1;
    while i <= last {
        if nums[i as usize] == val {
            nums.swap(i as usize, last as usize);
            last -= 1;
        } else {
            i += 1;
        }
    }
    last + 1
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/remove-element.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
