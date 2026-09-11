# Longest Increasing Subsequence

**Puzzle date:** 2026-07-14  
**Category:** dynamic programming  
**Time complexity:** `O(n log n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the outer for-loop that iterates over all n elements of nums, and inside each iteration you call bisect.bisect_left on the tails list, which performs a binary search in O(log n) time. Multiplying these together gives O(n log n) overall. The tails list grows at most to length n (in the worst case when the input is strictly increasing), so the space complexity is O(n). You might be tempted to say O(n²) because maintaining a list inside a loop can sometimes involve shifting elements, but here tails[i] = n is a single index assignment — no shifting occurs — so the per-iteration work is truly O(log n), not O(n).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
import bisect

def length_of_lis(nums: list[int]) -> int:
    tails = []
    for n in nums:
        i = bisect.bisect_left(tails, n)
        if i == len(tails):
            tails.append(n)
        else:
            tails[i] = n
    return len(tails)
```

### C++

```cpp
#include <vector>
#include <algorithm>

int lengthOfLIS(std::vector<int>& nums) {
    std::vector<int> tails;
    for (int n : nums) {
        auto it = std::lower_bound(tails.begin(), tails.end(), n);
        if (it == tails.end()) tails.push_back(n);
        else *it = n;
    }
    return tails.size();
}
```

### Rust

```rust
fn length_of_lis(nums: &[i32]) -> usize {
    let mut tails: Vec<i32> = Vec::new();
    for &n in nums {
        match tails.binary_search(&n) {
            Ok(i) => tails[i] = n,
            Err(i) => {
                if i == tails.len() {
                    tails.push(n);
                } else {
                    tails[i] = n;
                }
            }
        }
    }
    tails.len()
}
```

---

Played daily at [complexle.com](https://complexle.com).
