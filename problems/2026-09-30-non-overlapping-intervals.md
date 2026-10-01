# Non-overlapping Intervals

**Puzzle date:** 2026-09-30  
**Category:** arrays  
**Time complexity:** `O(n log n)`  
**Space complexity:** `O(log n)`

## Explanation

The dominant cost here is the sort call, since sorting n intervals by their end value takes O(n log n) time, which is more expensive than the single linear pass through the list that follows. You might be tempted to say O(n) because the for-loop only does constant work per iteration, but that loop's cost is dwarfed by the sort that happens first. The space usage comes from the sorting algorithm itself: Python's Timsort uses O(log n) auxiliary stack space for its merge operations, even though the sort is done in-place on the input list. A common wrong guess is O(1) space, but that ignores the internal overhead of the sorting algorithm.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def erase_overlap_intervals(intervals: list[list[int]]) -> int:
    intervals.sort(key=lambda interval: interval[1])
    result, right = 0, float("-inf")
    for l, r in intervals:
        if l < right:
            result += 1
        else:
            right = r
    return result
```

### C++

```cpp
int eraseOverlapIntervals(std::vector<std::vector<int>>& intervals) {
    std::sort(intervals.begin(), intervals.end(), [](const std::vector<int>& a, const std::vector<int>& b) { return a[1] < b[1]; });
    int result = 0, right = std::numeric_limits<int>::min();
    for (const auto& x : intervals) {
        if (x[0] < right) {
            ++result;
        } else {
            right = x[1];
        }
    }
    return result;
}
```

### Rust

```rust
fn erase_overlap_intervals(intervals: &mut Vec<Vec<i32>>) -> i32 {
    intervals.sort_by_key(|iv| iv[1]);
    let mut result = 0;
    let mut right = i32::MIN;
    for iv in intervals.iter() {
        if iv[0] < right {
            result += 1;
        } else {
            right = iv[1];
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/non-overlapping-intervals.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
