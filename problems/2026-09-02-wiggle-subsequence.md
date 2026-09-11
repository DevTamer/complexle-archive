# Wiggle Subsequence

**Puzzle date:** 2026-09-02  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The single for loop runs from index 1 to len(nums)-1, doing constant-time comparisons and updates each iteration, so the dominant cost is that one pass through the list, giving you O(n) time. There's no nested loop, recursion, or sorting involved, so you don't get any multiplicative or logarithmic factors. The most tempting wrong answer is O(n log n), which people often guess when they assume some sorting or divide-and-conquer step is hidden in the logic, but here it's just simple sequential scanning. For space, you only use a few scalar variables like length and up regardless of input size, so it's O(1) constant space, not O(n) which would apply if you stored an array or list proportional to the input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def wiggle_max_length(nums: list[int]) -> int:
    if len(nums) < 2:
        return len(nums)

    length = 1
    up: bool | None = None

    for i in range(1, len(nums)):
        if nums[i - 1] < nums[i] and (up is None or up is False):
            length += 1
            up = True
        elif nums[i - 1] > nums[i] and (up is None or up is True):
            length += 1
            up = False

    return length
```

### C++

```cpp
int wiggleMaxLength(std::vector<int>& nums) {
    if (nums.size() < 2) {
        return static_cast<int>(nums.size());
    }

    int length = 1;
    int up = 0; // 0 = none, 1 = true (up), -1 = false (down)

    for (int i = 1; i < static_cast<int>(nums.size()); ++i) {
        if (nums[i - 1] < nums[i] && (up == 0 || up == -1)) {
            ++length;
            up = 1;
        } else if (nums[i - 1] > nums[i] && (up == 0 || up == 1)) {
            ++length;
            up = -1;
        }
    }

    return length;
}
```

### Rust

```rust
fn wiggle_max_length(nums: &[i32]) -> i32 {
    if nums.len() < 2 {
        return nums.len() as i32;
    }

    let mut length = 1;
    let mut up: Option<bool> = None;

    for i in 1..nums.len() {
        if nums[i - 1] < nums[i] && (up.is_none() || up == Some(false)) {
            length += 1;
            up = Some(true);
        } else if nums[i - 1] > nums[i] && (up.is_none() || up == Some(true)) {
            length += 1;
            up = Some(false);
        }
    }

    length
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/wiggle-subsequence.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
