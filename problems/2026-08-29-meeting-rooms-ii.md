# Meeting Rooms II

**Puzzle date:** 2026-08-29  
**Category:** arrays  
**Time complexity:** `O(n log n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost here is the sort call on the 'line' list, which contains 2n entries (one start and one end event per interval). Sorting dominates because building the list and the final loop over it are both O(n), but comparison sorting takes O(n log n), and that term wins for large n. You might be tempted to say O(n) since the loop that computes 'result' only walks through the list once, but that overlooks the sort step that happens before it, which is the real bottleneck. For space, you need O(n) extra memory because the 'line' list stores two entries for every interval, proportional to the input size, plus whatever the sort algorithm uses internally. O(1) would be wrong because you're explicitly creating a new list of size 2n rather than working in place on the original intervals.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def min_meeting_rooms(intervals: list[list[int]]) -> int:
    line = [x for i, j in intervals for x in [[i, 1], [j, -1]]]
    line.sort()
    result, curr = 0, 0
    for _, num in line:
        curr += num
        result = max(result, curr)
    return result
```

### C++

```cpp
int minMeetingRooms(std::vector<std::vector<int>>& intervals) {
    std::vector<std::pair<int,int>> line;
    for (auto& iv : intervals) {
        line.push_back({iv[0], 1});
        line.push_back({iv[1], -1});
    }
    std::sort(line.begin(), line.end());
    int result = 0, curr = 0;
    for (auto& p : line) {
        curr += p.second;
        result = std::max(result, curr);
    }
    return result;
}
```

### Rust

```rust
fn min_meeting_rooms(intervals: &[Vec<i32>]) -> i32 {
    let mut line: Vec<(i32, i32)> = Vec::new();
    for iv in intervals {
        line.push((iv[0], 1));
        line.push((iv[1], -1));
    }
    line.sort();
    let mut result = 0;
    let mut curr = 0;
    for (_, num) in line {
        curr += num;
        result = result.max(curr);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/meeting-rooms-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
