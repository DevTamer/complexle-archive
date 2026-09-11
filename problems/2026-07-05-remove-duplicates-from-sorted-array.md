# Remove Duplicates from Sorted Array

**Puzzle date:** 2026-07-05  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single `for` loop that iterates through the array once with the `fast` pointer, from index 1 to len(nums)-1, giving you O(n) time. Each element is visited exactly once, and the work done per element (a comparison and at most one assignment) is constant. You might be tempted to think it's O(n²) because there are two pointers (`slow` and `fast`), but both pointers only move forward and never cause nested iteration — they traverse the array in a single pass. For space, the algorithm modifies the array in-place using only two integer variables (`slow` and `fast`) regardless of input size, so the extra space is O(1); you might mistakenly say O(n) thinking the output counts, but the array is given to you and no new data structure is allocated.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def remove_duplicates(nums: list[int]) -> int:
    if not nums:
        return 0
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1
```

### C++

```cpp
#include <vector>

int removeDuplicates(std::vector<int>& nums) {
    if (nums.empty()) return 0;
    int slow = 0;
    for (int fast = 1; fast < (int)nums.size(); fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    return slow + 1;
}
```

### Rust

```rust
fn remove_duplicates(nums: &mut Vec<i32>) -> usize {
    if nums.is_empty() {
        return 0;
    }
    let mut slow = 0;
    for fast in 1..nums.len() {
        if nums[fast] != nums[slow] {
            slow += 1;
            nums[slow] = nums[fast];
        }
    }
    slow + 1
}
```

---

Played daily at [complexle.com](https://complexle.com).
