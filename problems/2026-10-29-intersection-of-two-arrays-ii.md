# Intersection of Two Arrays II

**Puzzle date:** 2026-10-29  
**Category:** hash map  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(min(n, m))`

## Explanation

One pass builds a frequency map over the first array and a second pass walks the other array, doing constant-time dictionary operations at each step, so the time is proportional to the two lengths added together rather than multiplied. The tempting answer is O(n * m) by assuming each element of one array is searched for in the other, but the hash map removes that inner search entirely. Space is the subtle part: the first two lines swap the arguments so the smaller array is always the one turned into a map, which bounds the map at min(n, m) entries rather than the size of whichever array happened to be passed first.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def intersect(nums1: list[int], nums2: list[int]) -> list[int]:
    if len(nums1) > len(nums2):
        return intersect(nums2, nums1)

    lookup: dict[int, int] = {}
    for i in nums1:
        lookup[i] = lookup.get(i, 0) + 1

    res: list[int] = []
    for i in nums2:
        if lookup.get(i, 0) > 0:
            res.append(i)
            lookup[i] -= 1

    return res
```

### C++

```cpp
std::vector<int> intersect(std::vector<int>& nums1, std::vector<int>& nums2) {
    if (nums1.size() > nums2.size()) {
        return intersect(nums2, nums1);
    }

    std::unordered_map<int, int> lookup;
    for (const auto& i : nums1) {
        ++lookup[i];
    }

    std::vector<int> result;
    for (const auto& i : nums2) {
        if (lookup[i] > 0) {
            result.push_back(i);
            --lookup[i];
        }
    }

    return result;
}
```

### Rust

```rust
fn intersect(nums1: &[i32], nums2: &[i32]) -> Vec<i32> {
    if nums1.len() > nums2.len() {
        return intersect(nums2, nums1);
    }

    let mut lookup: HashMap<i32, i32> = HashMap::new();
    for &i in nums1 {
        *lookup.entry(i).or_insert(0) += 1;
    }

    let mut res = Vec::new();
    for &i in nums2 {
        if let Some(count) = lookup.get_mut(&i) {
            if *count > 0 {
                res.push(i);
                *count -= 1;
            }
        }
    }

    res
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/intersection-of-two-arrays-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
