# Rotate Array

**Puzzle date:** 2026-09-03  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the three calls to reverse, each of which swaps elements in place using a while loop that runs about half the length of its segment. Since the three reversed segments together cover the array exactly (once fully, then split into two parts), the total number of swap operations is proportional to n, giving you O(n) time overall. You might be tempted to think this is O(n log n) because reverse is called multiple times, but each call's cost is linear and they are called a constant number of times (three), so the total stays linear rather than compounding. Space-wise, the algorithm only swaps elements directly within the input list using a few index variables, without allocating any new arrays or recursive stack frames, so the space complexity is O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def rotate(nums: list[int], k: int) -> list[int]:
    def reverse(nums: list[int], start: int, end: int) -> None:
        while start < end:
            nums[start], nums[end - 1] = nums[end - 1], nums[start]
            start += 1
            end -= 1

    k %= len(nums)
    reverse(nums, 0, len(nums))
    reverse(nums, 0, k)
    reverse(nums, k, len(nums))
    return nums
```

### C++

```cpp
#include <vector>
#include <algorithm>

std::vector<int> rotate(std::vector<int>& nums, int k) {
    if (!nums.empty()) {
        k %= (int)nums.size();
        std::reverse(nums.begin(), nums.end());
        std::reverse(nums.begin(), nums.begin() + k);
        std::reverse(nums.begin() + k, nums.end());
    }
    return nums;
}
```

### Rust

```rust
fn rotate(nums: &mut Vec<i32>, k: i32) -> Vec<i32> {
    fn reverse(nums: &mut [i32], start: usize, end: usize) {
        let mut s = start;
        let mut e = end;
        while s < e {
            nums.swap(s, e - 1);
            s += 1;
            e -= 1;
        }
    }

    let n = nums.len();
    let k = (k as usize) % n;
    reverse(nums, 0, n);
    reverse(nums, 0, k);
    reverse(nums, k, n);
    nums.clone()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/rotate-array.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
