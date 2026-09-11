# Median of Two Sorted Arrays

**Puzzle date:** 2026-06-13  
**Category:** binary search  
**Time complexity:** `O(log(min(m,n)))`  
**Space complexity:** `O(1)`

## Explanation

The algorithm performs binary search on the smaller of the two arrays (length m after the swap), halving the search space each iteration, resulting in O(log(min(m,n))) time. Only a constant number of variables are used regardless of input size, so space complexity is O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def find_median_sorted_arrays(nums1: list[int], nums2: list[int]) -> float:
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1
    m, n = len(nums1), len(nums2)
    lo, hi = 0, m
    while lo <= hi:
        i = (lo + hi) // 2
        j = (m + n + 1) // 2 - i
        max_left1 = float('-inf') if i == 0 else nums1[i-1]
        min_right1 = float('inf') if i == m else nums1[i]
        max_left2 = float('-inf') if j == 0 else nums2[j-1]
        min_right2 = float('inf') if j == n else nums2[j]
        if max_left1 <= min_right2 and max_left2 <= min_right1:
            if (m + n) % 2 == 0:
                return (max(max_left1, max_left2) + min(min_right1, min_right2)) / 2
            return float(max(max_left1, max_left2))
        elif max_left1 > min_right2:
            hi = i - 1
        else:
            lo = i + 1
    raise ValueError("Input arrays are not sorted")
```

### C++

```cpp
double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
    if (nums1.size() > nums2.size()) std::swap(nums1, nums2);
    int m = nums1.size(), n = nums2.size();
    int lo = 0, hi = m;
    while (lo <= hi) {
        int i = (lo + hi) / 2;
        int j = (m + n + 1) / 2 - i;
        int ml1 = (i == 0) ? INT_MIN : nums1[i-1];
        int mr1 = (i == m) ? INT_MAX : nums1[i];
        int ml2 = (j == 0) ? INT_MIN : nums2[j-1];
        int mr2 = (j == n) ? INT_MAX : nums2[j];
        if (ml1 <= mr2 && ml2 <= mr1) {
            if ((m + n) % 2 == 0)
                return (std::max(ml1,ml2) + std::min(mr1,mr2)) / 2.0;
            return std::max(ml1, ml2);
        } else if (ml1 > mr2) hi = i - 1;
        else lo = i + 1;
    }
    return 0.0;
}
```

### Rust

```rust
fn find_median_sorted_arrays(nums1: &[i32], nums2: &[i32]) -> f64 {
    let (a, b) = if nums1.len() <= nums2.len() { (nums1, nums2) }
                 else { (nums2, nums1) };
    let (m, n) = (a.len(), b.len());
    let (mut lo, mut hi) = (0usize, m);
    while lo <= hi {
        let i = (lo + hi) / 2;
        let j = (m + n + 1) / 2 - i;
        let ml1 = if i == 0 { i32::MIN } else { a[i-1] };
        let mr1 = if i == m { i32::MAX } else { a[i] };
        let ml2 = if j == 0 { i32::MIN } else { b[j-1] };
        let mr2 = if j == n { i32::MAX } else { b[j] };
        if ml1 <= mr2 && ml2 <= mr1 {
            return if (m + n) % 2 == 0 {
                (ml1.max(ml2) as f64 + mr1.min(mr2) as f64) / 2.0
            } else { ml1.max(ml2) as f64 };
        } else if ml1 > mr2 { hi = i - 1; }
        else { lo = i + 1; }
    }
    0.0
}
```

---

Played daily at [complexle.com](https://complexle.com).
