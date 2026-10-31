# Intersection of Two Arrays

**Puzzle date:** 2026-10-30  
**Category:** hash map  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(min(n, m))`

## Explanation

Building the set from the first array is linear in its length, and the loop over the second array performs one constant-time membership test and at most one discard per element, so the total is proportional to n plus m rather than their product. The obvious wrong answer is O(n * m), which is what you would get with a nested scan instead of a set. Space is O(min(n, m)) rather than plain O(n): the guard at the top recurses with the arguments swapped so that the set is always built from the shorter array, capping the extra memory at the smaller of the two input sizes.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def intersection(nums1: list[int], nums2: list[int]) -> list[int]:
    if len(nums1) > len(nums2):
        return intersection(nums2, nums1)

    lookup = set(nums1)
    res = []
    for i in nums2:
        if i in lookup:
            res.append(i)
            lookup.discard(i)
    return res
```

### C++

```cpp
std::vector<int> intersection(std::vector<int>& nums1, std::vector<int>& nums2) {
    if (nums1.size() > nums2.size()) {
        return intersection(nums2, nums1);
    }

    std::unordered_set<int> lookup(nums1.begin(), nums1.end());

    std::vector<int> result;
    for (const auto& i : nums2) {
        if (lookup.count(i)) {
            result.push_back(i);
            lookup.erase(i);
        }
    }

    return result;
}
```

### Rust

```rust
fn intersection(nums1: &[i32], nums2: &[i32]) -> Vec<i32> {
    if nums1.len() > nums2.len() {
        return intersection(nums2, nums1);
    }

    let mut lookup: HashSet<i32> = nums1.iter().cloned().collect();

    let mut res = Vec::new();
    for &i in nums2 {
        if lookup.contains(&i) {
            res.push(i);
            lookup.remove(&i);
        }
    }

    res
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/intersection-of-two-arrays.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
