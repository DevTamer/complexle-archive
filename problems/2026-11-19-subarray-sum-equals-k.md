# Subarray Sum Equals K

**Puzzle date:** 2026-11-19  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The loop makes one pass over the array, and each iteration does a constant amount of work: one addition, one dictionary lookup, and one dictionary update. The prefix-sum map is what makes this linear — the brute-force alternative of checking every subarray would be O(n²), and that is the tempting answer here. Space is O(n) because the lookup dictionary records every distinct running sum encountered, and with all-distinct prefix sums that is one entry per element of the input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def subarray_sum(nums: list[int], k: int) -> int:
    result = 0
    accumulated_sum = 0
    lookup: dict[int, int] = {}
    lookup[0] = 1
    for num in nums:
        accumulated_sum += num
        result += lookup.get(accumulated_sum - k, 0)
        lookup[accumulated_sum] = lookup.get(accumulated_sum, 0) + 1
    return result
```

### C++

```cpp
int subarraySum(std::vector<int>& nums, int k) {
    int result = 0;
    int accumulated_sum = 0;
    std::unordered_map<int, int> lookup;
    ++lookup[0];
    for (const auto& num : nums) {
        accumulated_sum += num;
        result += lookup[accumulated_sum - k];
        ++lookup[accumulated_sum];
    }
    return result;
}
```

### Rust

```rust
fn subarray_sum(nums: &[i32], k: i32) -> i32 {
    let mut result = 0;
    let mut accumulated_sum = 0;
    let mut lookup: HashMap<i32, i32> = HashMap::new();
    lookup.insert(0, 1);
    for &num in nums {
        accumulated_sum += num;
        result += *lookup.get(&(accumulated_sum - k)).unwrap_or(&0);
        *lookup.entry(accumulated_sum).or_insert(0) += 1;
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/subarray-sum-equals-k.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
