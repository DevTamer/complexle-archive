# Single Number

**Puzzle date:** 2026-09-26  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the single for loop that iterates once over every element in nums, applying an XOR operation to combine it with result. Since each element is visited exactly once and the XOR operation itself takes constant time, the total work scales linearly with the size of the input, giving you O(n) time. You might be tempted to think this is O(1) because the operation per element looks trivial, but that ignores the fact that you still have to touch every item in the list at least once. For space, the function only uses a single integer variable, result, regardless of how large nums is, so no additional memory grows with input size, making the space complexity O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def single_number(nums: list[int]) -> int:
    result = 0
    for n in nums:
        result ^= n
    return result
```

### C++

```cpp
int singleNumber(std::vector<int>& nums) {
    return std::accumulate(nums.cbegin(), nums.cend(),
                            0, std::bit_xor<int>());
}
```

### Rust

```rust
fn single_number(nums: &[i32]) -> i32 {
    nums.iter().fold(0, |acc, &n| acc ^ n)
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/single-number.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
