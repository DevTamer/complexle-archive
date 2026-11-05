# Next Greater Element II

**Puzzle date:** 2026-11-04  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The outer loop runs 2n times to simulate wrapping around the circular array, which is still linear, and the inner while loop is a monotonic stack where each value is pushed once and popped at most once — so the inner work totals O(n) across the whole run rather than per iteration. The combination is O(n), not the O(n²) the nested loops suggest. Space is O(n): the result array holds one entry per element, and the stack can hold up to n values when the input is strictly increasing and nothing gets popped early.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def next_greater_elements(nums: list[int]) -> list[int]:
    n = len(nums)
    result, stk = [0] * n, []
    for i in reversed(range(2 * n)):
        while stk and stk[-1] <= nums[i % n]:
            stk.pop()
        result[i % n] = stk[-1] if stk else -1
        stk.append(nums[i % n])
    return result
```

### C++

```cpp
std::vector<int> nextGreaterElements(std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> result(n);
    std::stack<int> stk;
    for (int i = 2 * n - 1; i >= 0; --i) {
        while (!stk.empty() && stk.top() <= nums[i % n]) {
            stk.pop();
        }
        result[i % n] = stk.empty() ? -1 : stk.top();
        stk.push(nums[i % n]);
    }
    return result;
}
```

### Rust

```rust
fn next_greater_elements(nums: &[i32]) -> Vec<i32> {
    let n = nums.len();
    let mut result = vec![0; n];
    let mut stk: Vec<i32> = Vec::new();
    for i in (0..2 * n).rev() {
        let idx = i % n;
        while let Some(&top) = stk.last() {
            if top <= nums[idx] {
                stk.pop();
            } else {
                break;
            }
        }
        result[idx] = if let Some(&top) = stk.last() { top } else { -1 };
        stk.push(nums[idx]);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/next-greater-element-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
