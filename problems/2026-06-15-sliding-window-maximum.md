# Sliding Window Maximum

**Puzzle date:** 2026-06-15  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(k)`

## Explanation

Each element is added to and removed from the deque at most once across the entire iteration, making the total number of deque operations O(2n) = O(n). The space complexity is O(k) because the deque holds at most k indices at any given time, corresponding to the current sliding window, while the result array is not counted as auxiliary space.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
from collections import deque

def max_sliding_window(nums: list[int], k: int) -> list[int]:
    dq = deque()  # stores indices
    result = []
    for i, n in enumerate(nums):
        while dq and nums[dq[-1]] < n:
            dq.pop()
        dq.append(i)
        if dq[0] == i - k:
            dq.popleft()
        if i >= k - 1:
            result.append(nums[dq[0]])
    return result
```

### C++

```cpp
#include <vector>
#include <deque>

std::vector<int> maxSlidingWindow(std::vector<int>& nums, int k) {
    std::deque<int> dq;  // stores indices
    std::vector<int> result;
    for (int i = 0; i < (int)nums.size(); i++) {
        while (!dq.empty() && nums[dq.back()] < nums[i])
            dq.pop_back();
        dq.push_back(i);
        if (dq.front() == i - k)
            dq.pop_front();
        if (i >= k - 1)
            result.push_back(nums[dq.front()]);
    }
    return result;
}
```

### Rust

```rust
use std::collections::VecDeque;

fn max_sliding_window(nums: &[i32], k: usize) -> Vec<i32> {
    let mut dq: VecDeque<usize> = VecDeque::new();
    let mut result = Vec::new();
    for (i, &n) in nums.iter().enumerate() {
        while dq.back().map_or(false, |&j| nums[j] < n) {
            dq.pop_back();
        }
        dq.push_back(i);
        if dq.front() == Some(&(i.wrapping_sub(k))) {
            dq.pop_front();
        }
        if i >= k - 1 {
            result.push(nums[*dq.front().unwrap()]);
        }
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
