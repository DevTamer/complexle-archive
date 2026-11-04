# Largest Rectangle in Histogram

**Puzzle date:** 2026-11-03  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The inner while loop makes this look quadratic, but it is a monotonic stack: every index is pushed exactly once and popped at most once across the entire run, so the total number of inner iterations is bounded by n regardless of how many fire in any single outer step. Amortised over the outer loop that gives O(n), and O(n²) is precisely the trap the nested loops set. Space is O(n) for the stack, which in the worst case — a strictly increasing histogram, where nothing is ever popped until the end — holds an entry for every bar.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def largest_rectangle_area(heights: list[int]) -> int:
    stk: list[int] = [-1]
    result = 0
    for i in range(len(heights) + 1):
        while stk[-1] != -1 and (i == len(heights) or heights[stk[-1]] >= heights[i]):
            h = heights[stk.pop()]
            result = max(result, h * ((i - 1) - stk[-1]))
        stk.append(i)
    return result
```

### C++

```cpp
int largestRectangleArea(std::vector<int>& heights) {
    std::vector<int> stk = {-1};
    int result = 0;
    int n = static_cast<int>(heights.size());
    for (int i = 0; i <= n; ++i) {
        while (stk.back() != -1 && (i == n || heights[stk.back()] >= heights[i])) {
            int last = stk.back(); stk.pop_back();
            result = std::max(result, heights[last] * ((i - 1) - stk.back()));
        }
        stk.push_back(i);
    }
    return result;
}
```

### Rust

```rust
fn largest_rectangle_area(heights: &[i32]) -> i32 {
    let n = heights.len();
    let mut stk: Vec<i32> = vec![-1];
    let mut result = 0;
    for i in 0..=n {
        while *stk.last().unwrap() != -1
            && (i == n || heights[*stk.last().unwrap() as usize] >= heights[i])
        {
            let last = stk.pop().unwrap();
            let h = heights[last as usize];
            let top = *stk.last().unwrap();
            let width = (i as i32 - 1) - top;
            result = result.max(h * width);
        }
        stk.push(i as i32);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/largest-rectangle-in-histogram.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
