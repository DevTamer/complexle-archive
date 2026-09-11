# Two Sum II - Input Array Is Sorted

**Puzzle date:** 2026-09-01  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The while loop uses two pointers, start and end, that move toward each other, and in the worst case they traverse the array once before meeting, so the dominant cost is that single pass through nums. Each iteration does constant work (a comparison and pointer update), so the total work scales linearly with n, giving you O(n) time. You might be tempted to think O(n log n) because two-pointer techniques sometimes follow sorting, but here the array is already sorted and no sorting or extra searching happens. Space-wise, you only ever use a few variables like start, end, and total, none of which grow with input size, so the space stays constant at O(1) regardless of how big nums is.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def two_sum(nums: list[int], target: int) -> list[int]:
    start, end = 0, len(nums) - 1
    while start != end:
        total = nums[start] + nums[end]
        if total > target:
            end -= 1
        elif total < target:
            start += 1
        else:
            return [start + 1, end + 1]
    return []
```

### C++

```cpp
std::vector<int> twoSum(std::vector<int>& numbers, int target) {
    int left = 0, right = static_cast<int>(numbers.size()) - 1;
    while (left != right) {
        int sum = numbers[left] + numbers[right];
        if (sum > target) {
            --right;
        } else if (sum < target) {
            ++left;
        } else {
            return {left + 1, right + 1};
        }
    }
    return {};
}
```

### Rust

```rust
fn two_sum(numbers: &[i32], target: i32) -> Vec<i32> {
    let mut left: i32 = 0;
    let mut right: i32 = numbers.len() as i32 - 1;
    while left != right {
        let sum = numbers[left as usize] + numbers[right as usize];
        if sum > target {
            right -= 1;
        } else if sum < target {
            left += 1;
        } else {
            return vec![left + 1, right + 1];
        }
    }
    vec![]
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/two-sum-ii-input-array-is-sorted.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
