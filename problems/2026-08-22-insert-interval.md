# Insert Interval

**Puzzle date:** 2026-08-22  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost comes from the two while loops and the final extend, which together walk through the intervals list exactly once from start to end. You never revisit an element or sort anything, so each of the n intervals is processed with constant work, giving you a single linear pass. A tempting wrong answer is O(n log n), which people guess because interval problems often involve sorting, but this code assumes intervals are already sorted and never calls sort. For space, the result list can end up holding all n original intervals plus the merged one, so you need O(n) extra space rather than O(1), since the output isn't built in place.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def insert(intervals: list[list[int]], new_interval: list[int]) -> list[list[int]]:
    result = []
    i = 0
    n = len(intervals)
    while i < n and new_interval[0] > intervals[i][1]:
        result.append(intervals[i])
        i += 1
    while i < n and new_interval[1] >= intervals[i][0]:
        new_interval = [min(new_interval[0], intervals[i][0]),
                        max(new_interval[1], intervals[i][1])]
        i += 1
    result.append(new_interval)
    result.extend(intervals[i:])
    return result
```

### C++

```cpp
#include <vector>
#include <algorithm>

std::vector<std::vector<int>> insert(std::vector<std::vector<int>>& intervals, std::vector<int>& newInterval) {
    size_t i = 0;
    std::vector<std::vector<int>> result;
    while (i < intervals.size() && newInterval[0] > intervals[i][1]) {
        result.push_back(intervals[i]);
        i++;
    }
    while (i < intervals.size() && newInterval[1] >= intervals[i][0]) {
        newInterval = {std::min(newInterval[0], intervals[i][0]),
                       std::max(newInterval[1], intervals[i][1])};
        i++;
    }
    result.push_back(newInterval);
    for (; i < intervals.size(); i++) {
        result.push_back(intervals[i]);
    }
    return result;
}
```

### Rust

```rust
fn insert(intervals: &[Vec<i32>], new_interval: &[i32]) -> Vec<Vec<i32>> {
    let mut result = Vec::new();
    let mut i = 0;
    let n = intervals.len();
    let mut new_interval = new_interval.to_vec();
    while i < n && new_interval[0] > intervals[i][1] {
        result.push(intervals[i].clone());
        i += 1;
    }
    while i < n && new_interval[1] >= intervals[i][0] {
        new_interval = vec![
            new_interval[0].min(intervals[i][0]),
            new_interval[1].max(intervals[i][1]),
        ];
        i += 1;
    }
    result.push(new_interval);
    while i < n {
        result.push(intervals[i].clone());
        i += 1;
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/insert-interval.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
