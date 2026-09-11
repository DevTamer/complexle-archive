# Contains Duplicate

**Puzzle date:** 2026-07-01  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the single `for` loop that iterates over every element in `nums`, giving you a linear O(n) time complexity. Each iteration performs a set lookup (`n in seen`) and a set insertion (`seen.add(n)`), both of which are O(1) on average due to hashing, so the loop itself is the bottleneck. The most tempting wrong time answer might be O(1) because you see early returns, but in the worst case (no duplicates), you must visit every element. For space, the `seen` set grows as you add unique elements, and in the worst case it holds all n elements, so space is O(n) — not O(1) as you might assume if you mistakenly think the set stays small.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def contains_duplicate(nums: list[int]) -> bool:
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False
```

### C++

```cpp
#include <vector>
#include <unordered_set>

bool containsDuplicate(std::vector<int>& nums) {
    std::unordered_set<int> seen;
    for (int n : nums) {
        if (seen.count(n)) return true;
        seen.insert(n);
    }
    return false;
}
```

### Rust

```rust
use std::collections::HashSet;

fn contains_duplicate(nums: &[i32]) -> bool {
    let mut seen = HashSet::new();
    for &n in nums {
        if !seen.insert(n) {
            return true;
        }
    }
    false
}
```

---

Played daily at [complexle.com](https://complexle.com).
