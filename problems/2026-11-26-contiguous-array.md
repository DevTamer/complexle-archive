# Contiguous Array

**Puzzle date:** 2026-11-26  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the single pass over nums, where each step does a constant amount of work plus one hash map lookup or insert. Dictionary operations take average O(1) time, so n iterations give O(n) total time. The lookup dictionary stores the first index of each distinct running count, and the count can range from -n to n, so in the worst case (all 0s or all 1s) it holds about n entries, giving O(n) space. You might be tempted by O(n²), since the brute-force approach checks every subarray, but the prefix-count trick avoids nested loops entirely. You might also guess O(1) space because only a few scalar variables appear, but the dictionary grows with the input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def find_max_length(nums: list[int]) -> int:
    result = 0
    count = 0
    lookup = {0: -1}
    for i, num in enumerate(nums):
        count += 1 if num == 1 else -1
        if count in lookup:
            result = max(result, i - lookup[count])
        else:
            lookup[count] = i
    return result
```

### C++

```cpp
int findMaxLength(std::vector<int>& nums) {
    int result = 0, count = 0;
    std::unordered_map<int, int> lookup;
    lookup[0] = -1;
    for (int i = 0; i < (int)nums.size(); i++) {
        count += nums[i] == 1 ? 1 : -1;
        if (lookup.count(count)) {
            result = std::max(result, i - lookup[count]);
        } else {
            lookup[count] = i;
        }
    }
    return result;
}
```

### Rust

```rust
fn find_max_length(nums: &[i32]) -> i32 {
    let mut result: i32 = 0;
    let mut count: i32 = 0;
    let mut lookup: HashMap<i32, i32> = HashMap::new();
    lookup.insert(0, -1);
    for (i, &num) in nums.iter().enumerate() {
        count += if num == 1 { 1 } else { -1 };
        let i = i as i32;
        if let Some(&j) = lookup.get(&count) {
            result = result.max(i - j);
        } else {
            lookup.insert(count, i);
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/contiguous-array.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
