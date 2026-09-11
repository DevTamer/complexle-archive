# Product of Array Except Self

**Puzzle date:** 2026-06-19  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the two separate for-loops, each iterating over all n elements once. Because these loops run sequentially rather than nested, the total work is 2n, which simplifies to O(n). For space, you might be tempted to say O(n) because of the 'result' array, but that array holds the output that the problem itself requires you to return — it is not auxiliary/extra space. The only additional variables used are the scalar 'left', 'right', and 'i', which are O(1). So the extra space beyond the output is O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def product_except_self(nums: list[int]) -> list[int]:
    n = len(nums)
    result = [1] * n
    left = 1
    for i in range(n):
        result[i] = left
        left *= nums[i]
    right = 1
    for i in range(n - 1, -1, -1):
        result[i] *= right
        right *= nums[i]
    return result
```

### C++

```cpp
std::vector<int> productExceptSelf(std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> result(n, 1);
    int left = 1;
    for (int i = 0; i < n; i++) {
        result[i] = left;
        left *= nums[i];
    }
    int right = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= right;
        right *= nums[i];
    }
    return result;
}
```

### Rust

```rust
fn product_except_self(nums: &[i32]) -> Vec<i32> {
    let n = nums.len();
    let mut result = vec![1i32; n];
    let mut left = 1;
    for i in 0..n {
        result[i] = left;
        left *= nums[i];
    }
    let mut right = 1;
    for i in (0..n).rev() {
        result[i] *= right;
        right *= nums[i];
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
