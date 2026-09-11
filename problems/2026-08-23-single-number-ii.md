# Single Number II

**Puzzle date:** 2026-08-23  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The single for loop iterates once over each element in nums, and inside the loop only constant-time bitwise operations are performed to update one and two. Since the work per element doesn't depend on the size of the list and there's no nested iteration or sorting, the total cost scales linearly with n, giving O(n) time. You might be tempted to say O(1) since the operations look trivial, but that ignores that you still have to visit every element of the input at least once. For space, only two integer variables (one and two) are used regardless of how large nums is, so no additional memory grows with input size, making it O(1) space rather than O(n), which would apply if you were storing extra data structures like a hash set.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def single_number(nums: list[int]) -> int:
    one, two = 0, 0
    for x in nums:
        one, two = (~x & one) | (x & ~one & ~two), (~x & two) | (x & one)
    return one
```

### C++

```cpp
int singleNumber(std::vector<int>& nums) {
    int one = 0, two = 0;
    for (int i : nums) {
        int new_one = (~i & one) | (i & ~one & ~two);
        int new_two = (~i & two) | (i & one);
        one = new_one;
        two = new_two;
    }
    return one;
}
```

### Rust

```rust
fn single_number(nums: &[i32]) -> i32 {
    let mut one: i32 = 0;
    let mut two: i32 = 0;
    for &x in nums {
        let new_one = (!x & one) | (x & !one & !two);
        let new_two = (!x & two) | (x & one);
        one = new_one;
        two = new_two;
    }
    one
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/single-number-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
