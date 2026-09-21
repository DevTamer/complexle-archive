# Subarray Product Less Than K

**Puzzle date:** 2026-09-20  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

You should focus on the two pointers, start and i, which both move only forward through nums using a sliding window. Even though there's a while loop nested inside the for loop, start never resets and can only advance up to n times total across the entire run, so the combined work of both loops is still bounded by O(n), not O(n²). The most tempting wrong answer is O(n²), which people pick because they see a nested loop and assume it multiplies the cost, but that ignores that the inner loop's total iterations across all outer iterations are capped by n. Space-wise, the code only uses a few scalar variables like result, start, and prod, with no arrays, sets, or recursion stacks that grow with input size, so space stays constant at O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def num_subarray_product_less_than_k(nums: list[int], k: int) -> int:
    if k <= 1:
        return 0
    result, start, prod = 0, 0, 1
    for i, num in enumerate(nums):
        prod *= num
        while prod >= k:
            prod //= nums[start]
            start += 1
        result += i - start + 1
    return result
```

### C++

```cpp
int numSubarrayProductLessThanK(std::vector<int>& nums, int k) {
    if (k <= 1) return 0;
    int result = 0, start = 0, prod = 1;
    for (int i = 0; i < (int)nums.size(); ++i) {
        prod *= nums[i];
        while (prod >= k) {
            prod /= nums[start];
            ++start;
        }
        result += i - start + 1;
    }
    return result;
}
```

### Rust

```rust
fn num_subarray_product_less_than_k(nums: &[i32], k: i32) -> i32 {
    if k <= 1 {
        return 0;
    }
    let mut result: i32 = 0;
    let mut start: usize = 0;
    let mut prod: i32 = 1;
    for i in 0..nums.len() {
        prod *= nums[i];
        while prod >= k {
            prod /= nums[start];
            start += 1;
        }
        result += (i as i32) - (start as i32) + 1;
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/subarray-product-less-than-k.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
