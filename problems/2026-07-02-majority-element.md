# Majority Element

**Puzzle date:** 2026-07-02  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single for-loop that iterates over every element in nums exactly once, giving you O(n) time. Each iteration does a fixed amount of work — just a comparison and an increment or decrement — so nothing inside the loop adds extra complexity. You might be tempted to think this is O(n²) if you imagine some hidden nested scanning, but there is none; the Boyer-Moore Voting Algorithm is specifically designed to find the majority in one linear pass. For space, you only ever allocate two scalar variables (count and candidate) regardless of how large nums is, so space stays O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def majority_element(nums: list[int]) -> int:
    count = 0
    candidate = None
    for n in nums:
        if count == 0:
            candidate = n
        count += 1 if n == candidate else -1
    return candidate
```

### C++

```cpp
#include <vector>

int majorityElement(std::vector<int>& nums) {
    int count = 0, candidate = 0;
    for (int n : nums) {
        if (count == 0) candidate = n;
        count += (n == candidate) ? 1 : -1;
    }
    return candidate;
}
```

### Rust

```rust
fn majority_element(nums: &[i32]) -> i32 {
    let mut count = 0;
    let mut candidate = 0;
    for &n in nums {
        if count == 0 {
            candidate = n;
        }
        count += if n == candidate { 1 } else { -1 };
    }
    candidate
}
```

---

Played daily at [complexle.com](https://complexle.com).
