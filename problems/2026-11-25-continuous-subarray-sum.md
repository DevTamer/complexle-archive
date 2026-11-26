# Continuous Subarray Sum

**Puzzle date:** 2026-11-25  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(min(n, k))`

## Explanation

A single pass maintains a running sum and does one constant-time dictionary lookup and insert per element, so the time is linear — the brute force of summing every subarray would be the O(n²) alternative. Space is the subtle half: the dictionary is keyed by the running sum taken modulo k, and there are only k possible remainders, so the map can never exceed k entries no matter how long the array is. It also cannot exceed n entries, since at most one is stored per element, making the true bound the smaller of the two: O(min(n, k)).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def check_subarray_sum(nums: list[int], k: int) -> bool:
    count = 0
    lookup: dict[int, int] = {0: -1}
    for i, num in enumerate(nums):
        count += num
        if k:
            count %= k
        if count in lookup:
            if i - lookup[count] > 1:
                return True
        else:
            lookup[count] = i
    return False
```

### C++

```cpp
bool checkSubarraySum(std::vector<int>& nums, int k) {
    int count = 0;
    std::unordered_map<int, int> lookup;
    lookup[0] = -1;
    for (int i = 0; i < (int)nums.size(); ++i) {
        count += nums[i];
        if (k != 0) {
            count %= k;
        }
        if (lookup.count(count)) {
            if (i - lookup[count] > 1) {
                return true;
            }
        } else {
            lookup[count] = i;
        }
    }
    return false;
}
```

### Rust

```rust
fn check_subarray_sum(nums: &[i32], k: i32) -> bool {
    let mut count: i32 = 0;
    let mut lookup: HashMap<i32, i32> = HashMap::new();
    lookup.insert(0, -1);
    for (i, &num) in nums.iter().enumerate() {
        count += num;
        if k != 0 {
            count %= k;
        }
        if let Some(&prev) = lookup.get(&count) {
            if (i as i32) - prev > 1 {
                return true;
            }
        } else {
            lookup.insert(count, i as i32);
        }
    }
    false
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/continuous-subarray-sum.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
