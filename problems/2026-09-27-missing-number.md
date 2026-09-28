# Missing Number

**Puzzle date:** 2026-09-27  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The single for loop using enumerate walks through nums exactly once, doing a constant-time XOR operation on each pass, so the dominant cost is that one linear scan giving you O(n) time. There's no nested loop, sorting, or recursive call anywhere in the code, which is why something like O(n log n) doesn't apply even though sorting-based solutions to this same problem exist. For space, you only ever update a single variable called result, and no extra list, set, or recursion stack is created, so the space stays constant at O(1) regardless of how large nums gets. The most tempting wrong answer is O(n) space, since it's easy to assume any array-processing function needs auxiliary storage proportional to input size, but here the algorithm cleverly reuses XOR properties instead of building any new data structure.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def missing_number(nums: list[int]) -> int:
    result = len(nums)
    for i, n in enumerate(nums):
        result ^= i ^ n
    return result
```

### C++

```cpp
int missingNumber(std::vector<int>& nums) {
    int num = 0;
    for (int i = 0; i < (int)nums.size(); ++i) {
        num ^= nums[i] ^ (i + 1);
    }
    return num;
}
```

### Rust

```rust
fn missing_number(nums: &[i32]) -> i32 {
    let mut num = nums.len() as i32;
    for (i, &n) in nums.iter().enumerate() {
        num ^= (i as i32) ^ n;
    }
    num
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/missing-number.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
