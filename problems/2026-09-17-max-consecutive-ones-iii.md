# Max Consecutive Ones III

**Puzzle date:** 2026-09-17  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

You should focus on the two pointers i and j moving through the array. The outer for-loop advances j once per element, and the inner while-loop only advances i, which never resets and never exceeds n total steps across the whole run. Because both pointers together make at most 2n moves, the total work is linear, giving O(n) time. It's tempting to see the nested while inside the for-loop and assume O(n²), but that ignores that i only moves forward monotonically, so its total movement across all iterations is bounded by n, not n per outer iteration. Space stays O(1) since you only use a few scalar variables (result, i, k) and no extra data structures that scale with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def longest_ones(nums: list[int], k: int) -> int:
    result, i = 0, 0
    for j, n in enumerate(nums):
        k -= int(n == 0)
        while k < 0:
            k += int(nums[i] == 0)
            i += 1
        result = max(result, j - i + 1)
    return result
```

### C++

```cpp
int longestOnes(std::vector<int>& nums, int k) {
    int result = 0, i = 0;
    for (int j = 0; j < (int)nums.size(); ++j) {
        k -= (nums[j] == 0) ? 1 : 0;
        while (k < 0) {
            k += (nums[i] == 0) ? 1 : 0;
            ++i;
        }
        result = std::max(result, j - i + 1);
    }
    return result;
}
```

### Rust

```rust
fn longest_ones(nums: &[i32], k: i32) -> i32 {
    let mut k = k;
    let mut result: i32 = 0;
    let mut i: usize = 0;
    for j in 0..nums.len() {
        if nums[j] == 0 {
            k -= 1;
        }
        while k < 0 {
            if nums[i] == 0 {
                k += 1;
            }
            i += 1;
        }
        let len = (j - i + 1) as i32;
        if len > result {
            result = len;
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/max-consecutive-ones-iii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
