# Koko Eating Bananas

**Puzzle date:** 2026-11-20  
**Category:** binary search  
**Time complexity:** `O(n log m)`  
**Space complexity:** `O(1)`

## Explanation

The binary search is not over the array but over the answer: the candidate eating speeds run from 1 to the largest pile, so the loop halves that numeric range and runs about log m times, where m is the maximum pile size. Each check calls possible, which sums over every pile for O(n) work, giving O(n log m) in total. Note this is not O(n log n) — the log factor is driven by the size of the largest pile, not by how many piles there are. Space is O(1): possible uses a generator expression rather than building a list, so no memory scales with the input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def min_eating_speed(piles: list[int], h: int) -> int:
    def possible(k: int) -> bool:
        return sum((pile - 1) // k + 1 for pile in piles) <= h

    left, right = 1, max(piles)
    while left <= right:
        mid = left + (right - left) // 2
        if possible(mid):
            right = mid - 1
        else:
            left = mid + 1
    return left
```

### C++

```cpp
bool possible(const std::vector<int>& piles, int h, int k) {
    int time = 0;
    for (const auto& pile : piles) {
        time += (pile - 1) / k + 1;
    }
    return time <= h;
}

int minEatingSpeed(std::vector<int>& piles, int h) {
    int left = 1, right = *std::max_element(piles.cbegin(), piles.cend());
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (possible(piles, h, mid)) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

### Rust

```rust
fn possible(piles: &[i32], h: i32, k: i32) -> bool {
    let time: i32 = piles.iter().map(|&pile| (pile - 1) / k + 1).sum();
    time <= h
}

fn min_eating_speed(piles: &[i32], h: i32) -> i32 {
    let mut left = 1;
    let mut right = *piles.iter().max().unwrap();
    while left <= right {
        let mid = left + (right - left) / 2;
        if possible(piles, h, mid) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    left
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/koko-eating-bananas.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
