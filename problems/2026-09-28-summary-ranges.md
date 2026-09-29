# Summary Ranges

**Puzzle date:** 2026-09-28  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The single for loop iterates once through the array (n+1 times total, but that's still linear), and each iteration does constant-time work like comparisons and appending to a list, so the dominant cost is that one pass over nums, giving you O(n) time. You might be tempted to think O(n log n) because ranges sound like they need sorting, but there's no sorting or divide-and-conquer step here, just a straightforward scan. For space, the output list 'ranges' can grow to hold up to n separate range strings in the worst case (when no numbers are consecutive), so the space used to store the result scales linearly with n, making it O(n) rather than O(1). It's easy to mistakenly call this O(1) space if you only count the few extra variables like start and end and forget that the returned list itself counts toward space complexity.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def summary_ranges(nums: list[int]) -> list[str]:
    ranges = []
    if not nums:
        return ranges

    start = end = nums[0]
    for i in range(1, len(nums) + 1):
        if i < len(nums) and nums[i] == end + 1:
            end = nums[i]
        else:
            interval = str(start)
            if start != end:
                interval += "->" + str(end)
            ranges.append(interval)
            if i < len(nums):
                start = end = nums[i]

    return ranges
```

### C++

```cpp
std::vector<std::string> summaryRanges(std::vector<int>& nums) {
    std::vector<std::string> ranges;
    if (nums.empty()) {
        return ranges;
    }

    int start = nums[0], end = nums[0];
    for (int i = 1; i <= (int)nums.size(); ++i) {
        if (i < (int)nums.size() && nums[i] == end + 1) {
            end = nums[i];
        } else {
            std::string range = std::to_string(start);
            if (start != end) {
                range += "->" + std::to_string(end);
            }
            ranges.push_back(range);
            if (i < (int)nums.size()) {
                start = end = nums[i];
            }
        }
    }

    return ranges;
}
```

### Rust

```rust
fn summary_ranges(nums: &[i32]) -> Vec<String> {
    let mut ranges = Vec::new();
    if nums.is_empty() {
        return ranges;
    }

    let mut start = nums[0];
    let mut end = nums[0];
    for i in 1..=nums.len() {
        if i < nums.len() && nums[i] == end + 1 {
            end = nums[i];
        } else {
            let mut interval = start.to_string();
            if start != end {
                interval.push_str(&format!("->{}", end));
            }
            ranges.push(interval);
            if i < nums.len() {
                start = nums[i];
                end = nums[i];
            }
        }
    }

    ranges
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/summary-ranges.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
