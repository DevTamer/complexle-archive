# First Missing Positive

**Puzzle date:** 2026-08-20  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the cyclic-sort style while loop that swaps each number into its correct index position. Although it looks nested inside a for loop, each swap places at least one value into its final correct slot permanently, so across the entire array at most n swaps can ever happen in total, making the whole first loop O(n) amortized rather than O(n²). The second loop is a simple single pass over the array, also O(n), so the overall time stays linear. The most tempting wrong answer is O(n²) because of the nested while-inside-for structure, but that ignores the fact that swaps are bounded by n total, not n per outer iteration. Space is O(1) because the algorithm rearranges numbers in place using only a few index variables, without allocating any extra arrays or data structures that scale with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def first_missing_positive(nums: list[int]) -> int:
    n = len(nums)
    for i in range(n):
        while 1 <= nums[i] <= n and nums[nums[i] - 1] != nums[i]:
            nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]
    for i in range(n):
        if nums[i] != i + 1:
            return i + 1
    return n + 1
```

### C++

```cpp
#include <vector>
#include <utility>

int firstMissingPositive(std::vector<int>& nums) {
    int n = nums.size();
    for (int i = 0; i < n; i++) {
        while (nums[i] >= 1 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
            std::swap(nums[nums[i] - 1], nums[i]);
        }
    }
    for (int i = 0; i < n; i++) {
        if (nums[i] != i + 1) {
            return i + 1;
        }
    }
    return n + 1;
}
```

### Rust

```rust
fn first_missing_positive(nums: &mut Vec<i32>) -> i32 {
    let n = nums.len() as i32;
    for i in 0..nums.len() {
        while nums[i] >= 1 && nums[i] <= n && nums[(nums[i] - 1) as usize] != nums[i] {
            let j = (nums[i] - 1) as usize;
            nums.swap(i, j);
        }
    }
    for i in 0..nums.len() {
        if nums[i] != (i as i32 + 1) {
            return i as i32 + 1;
        }
    }
    n + 1
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/first-missing-positive.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
