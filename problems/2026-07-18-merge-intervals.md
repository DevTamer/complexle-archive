# Merge Intervals

**Puzzle date:** 2026-07-18  
**Category:** sorting  
**Time complexity:** `O(n log n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the sort at the start of the function, which takes O(n log n) time for n intervals. After sorting, the single for-loop runs through all intervals exactly once, giving O(n) work — but since O(n log n) grows faster, the sort dominates the overall time complexity. You might be tempted to say O(n) because the loop is so simple and linear, but you cannot ignore the sort that happens before it. For space, the result list can hold up to n intervals in the worst case (when no intervals overlap), giving O(n) auxiliary space; the sort itself may also use O(log n) stack space, but O(n) dominates.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def merge_intervals(intervals: list[list[int]]) -> list[list[int]]:
    intervals.sort(key=lambda x: x[0])
    result = []
    for start, end in intervals:
        if result and start <= result[-1][1]:
            result[-1][1] = max(result[-1][1], end)
        else:
            result.append([start, end])
    return result
```

### C++

```cpp
#include <vector>
#include <algorithm>

std::vector<std::vector<int>> mergeIntervals(std::vector<std::vector<int>>& intervals) {
    std::sort(intervals.begin(), intervals.end());
    std::vector<std::vector<int>> result;
    for (auto& interval : intervals) {
        if (!result.empty() && interval[0] <= result.back()[1]) {
            result.back()[1] = std::max(result.back()[1], interval[1]);
        } else {
            result.push_back(interval);
        }
    }
    return result;
}
```

### Rust

```rust
fn merge_intervals(mut intervals: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
    intervals.sort_by_key(|iv| iv[0]);
    let mut result: Vec<Vec<i32>> = Vec::new();
    for interval in intervals {
        if let Some(last) = result.last_mut() {
            if interval[0] <= last[1] {
                last[1] = last[1].max(interval[1]);
                continue;
            }
        }
        result.push(interval);
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
